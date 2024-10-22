# App 

Na platformě OSCloud nabízíme předinstalované i volně dostupné aplikace, které můžete snadno spravovat přímo z našeho uživatelského rozhraní.

## Předinstalované aplikace

Tyto aplikace jsou již připravené k okamžitému použití:

- Mastodon: Decentralizovaná sociální síť.
- Pixelfed: Platforma pro sdílení fotografií.
- Nextcloud: Soukromý cloud pro ukládání a sdílení souborů.
- Nástroje pro produktivitu: CryptPad, HedgeDoc pro týmovou spolupráci a organizaci projektů.


## Další dostupné aplikace k instalaci

Pokud potřebujete další aplikace, můžete je kdykoli snadno nainstalovat přímo z našeho App Storu. K dispozici jsou například:

- Fotografické aplikace: Lychee, Piwigo pro správu a sdílení fotografií.
- Webové aplikace: WordPress, Surfer pro tvorbu a správu webových stránek.

S OSCloud máte plnou kontrolu nad tím, jaké aplikace potřebujete pro svůj projekt, a všechny aplikace jsou pravidelně aktualizovány a bezpečně spravovány.

Chcete-li zobrazit kompletní seznam aplikací, navštivte [Aplikace](aplikace.md).

### Ikona

V sekci `Ikona` můžete nastavit vlastní ikonu pro aplikaci. Pokud ikona není nastavena, použije se ikona balíčku aplikace. 

<center>
<img src="/img/ikon.png" class="shadow" width="250px">
</center>

### Operátor

Administrátor může nastavit uživatele nebo skupiny jako operátory aplikace. Operátor aplikace může provádět konfigurační a údržbové úkoly. Na rozdíl od administrátora aplikace nemůže operátor aplikaci odinstalovat ani změnit její umístění. Operátoři také nemohou klonovat aplikace, protože nemají oprávnění k instalaci nových aplikací.

Operátor uvidí na svém panelu ikonu ozubeného kola: 

<center>
<img src="/img/apps-operator-button.png" class="shadow" width="250px">
</center>

Po kliknutí na ikonu ozubeného kola se jim zobrazí uživatelské rozhraní operátora: 

<center>
<img src="/img/apps-operator-view.png" class="shadow" width="600px">
</center>

## Informace

Různé informace o aplikaci naleznete v sekci `Info` aplikace:

<center>
<img src="/img/apps-info.png" class="shadow" width="600px">
</center>


* `Název a verze aplikace` - Toto je název aplikace a verze upstream aplikace.
* `App ID` - Unikátní ID instance aplikace.
* `Verze balíčku` - Verze balíčku OSCloud, která je odlišná od verze aplikace.
* `Nainstalováno` - Datum instalace aplikace.
* `Poslední aktualizace` - Kdy byla aplikace naposledy aktualizována.

### Poznámky admina

Poznámky specifické pro aplikaci lze uložit ve formátu Markdown. Poznámky jsou sdílené mezi administrátory. Všichni administrátoři a [operátoři aplikací](#operators) je mohou zobrazit a upravovat.

<center>
<img src="/img/apps-admin-notes.png" class="shadow" width="600px">
</center>


## Zabezpečení

### robots.txt

Soubor `Robots.txt` je soubor sloužící k určení, které části webu by měl vyhledávač indexovat. Tento soubor se řídí
[Robots Exclusion Standardem](https://cs.wikipedia.org/wiki/Robots_exclusion_standard). Google má 
[skvělý dokument](https://developers.google.com/search/reference/robots_txt) o tom, jak robots.txt funguje.

Obsah souboru robots.txt pro aplikaci můžete nastavit v sekci `Zabezpečení` v uživatelském rozhraní aplikace.

Ve výchozím nastavení OSCloud nenastavuje robots.txt pro aplikace. Pokud není nastaven, aplikace si může poskytovat vlastní robots.txt.

<center>
<img src="/img/apps-robots-txt.png" class="shadow" width="600px">
</center>

Kromě toho má stránka administrace OSCloud vlastní robots.txt, který zakazuje indexování:

```bash
User-agent: *
Disallow: /
```

### HSTS Preload

[HSTS Preload](https://hstspreload.org/) je seznam stránek, které jsou v prohlížečích jako Chrome, Firefox, Opera a další hardcodovány jako HTTPS-only.

Požadavky a důsledky:

* Vzhledem k velikosti seznamu jsou akceptovány automatické žádosti o přidání celých domén (hlavní doména).
* To zabrání přístupu ke všem subdoménám bez platného certifikátu HTTPS.
* Nové položky jsou hardcodovány do zdrojového kódu prohlížeče Chrome a může trvat několik měsíců, než se dostanou do stabilní verze.

Po aktivaci OSCloud bude server zasílat následující hlavičky HSTS:

```
Strict-Transport-Security: max-age=63072000; includeSubDomains; preload
```

Pro aktivaci HSTS Preload tuto možnost zapněte v sekci `Zabezpečení` aplikace:

<center>
<img src="/img/apps-security-hsts-preload.png" class="shadow" width="600px">
</center>

!!! note "Odeslání"
    OSCloud automaticky neodesílá doménu na seznam HSTS Preload. To musíte provést ručně [zde](https://hstspreload.org/).

## Cron

Cron úlohy, které aplikace potřebují k fungování, jsou již integrovány do balíčku aplikace a není potřeba další konfigurace. Pokud chcete spustit další vlastní příkazy cron, můžete je přidat v sekci `Cron`.

Příkazy cron jsou spuštěny ve stejném kontextu jako aplikace (v samostatném kontejneru). To znamená, že mají přístup ke stejným prostředím a databázím jako aplikace. Sledují také životní cyklus aplikace – pokud je aplikace zastavena, cron úlohy se nespouštějí. Výstup z cron příkazů lze prohlížet pomocí [prohlížeče logů](#log-viewer).

Časy v cron jsou specifikovány v UTC.

Vzorový vzor plánu může být jeden z následujících [rozšíření cron](https://www.man7.org/linux/man-pages/man5/crontab.5.html#EXTENSIONS):

* `@service`   :    Spustí jednou při restartu aplikace nebo pokud je aplikace již spuštěná.
* `@reboot `   :    Spustí jednou při restartu aplikace nebo pokud je aplikace již spuštěná.
* `@yearly`    :    Spustí jednou ročně, např. `0 0 1 1 *`.
* `@annually`  :    Spustí jednou ročně, např. `0 0 1 1 *`.
* `@monthly`   :    Spustí jednou měsíčně, např. `0 0 1 * *`.
* `@weekly`    :    Spustí jednou týdně, např. `0 0 * * 0`.
* `@daily`     :    Spustí jednou denně, např. `0 0 * * *`.
* `@hourly`    :    Spustí jednou za hodinu, např. `0 * * * *`.

<center>
<img src="/img/apps-cron.png" class="shadow" width="600px">
</center>

!!! note "Řetězení příkazů"
    Příkazy mohou být spojeny pomocí `&&` nebo `||`. Například: `echo "=> Doing job" && /app/data/do_job.sh`

## Webový Terminál

OSCloud poskytuje webový terminál, který umožňuje přístup k souborovému systému aplikace. Webový terminál lze použít k prohlížení a úpravám souborů aplikace, přístupu k databázi atd. OSCloud spouští aplikace jako kontejnery s režimem souborového systému pouze pro čtení. Pouze adresáře `/run` (dynamická data), `/app/data` (zálohovaná data) a `/tmp` (dočasné soubory) jsou zapisovatelné.

Webový terminál lze otevřít pomocí tlačítka Web Terminal:

<center>
<img src="/img/apps-terminal-button.png" class="shadow" width="400px">
</center>

Po kliknutí se otevře nové okno. Terminál je v podstatě shell do souborového systému aplikace.

<center>
<img src="/img/apps-terminal-exec2.png" class="shadow" width="600px">
</center>

## Správce souborů

OSCloud poskytuje Správce souborů, který lze použít k úpravě souborového systému aplikace přímo z prohlížeče.

Správce souborů lze otevřít pomocí tlačítka File Manager:

<center>
<img src="/img/apps-filemanager-button.png" class="shadow" width="600px">
</center>

Po kliknutí se otevře nové okno. V kontextové nabídce jsou dostupné akce jako Přejmenovat, Smazat, Změnit vlastnictví.

<center>
<img src="/img/filemanager.png" class="shadow" width="600px">
</center>

## Přístup přes SFTP

Některé aplikace, jako WordPress, LAMP, Surfer, podporují přístup k datům přes SFTP. Soubory lze prohlížet a nahrávat pomocí libovolného SFTP klienta. Informace o připojení k SFTP lze zobrazit kliknutím na položku menu `SFTP Access`.

<center>
<img src="/img/apps-sftp-info.png" class="shadow" width="600px">
</center>

SFTP klient, jako je například [FileZilla](https://filezilla-project.org/), lze použít k připojení následovně:

* `Host` - `sftp://my.cloudron.space` (hostitel je stejný pro přístup SFTP ke všem aplikacím)
* `Username` - `girish@lamp.cloudron.space` (uživatelské jméno je specifické pro každou aplikaci)
* `Password` - heslo do OSCloud (stejné heslo pro přístup SFTP ke všem aplikacím)
* `Port` - 222

<center>
<img src="/img/sftp-filezilla.png" class="shadow" width="600px">
</center>

Pouze administrátoři OSCloud mají přístup přes SFTP.

!!! note "Port 222"
    SFTP služba běží na portu 222. Firewall serveru má již tento port otevřený. Nicméně budete muset tento port povolit i ve firewallu poskytovatele hostingu (např. EC2 Security Group nebo DigitalOcean Firewall). Pokud je doména frontovaná přes Cloudflare, použijte IP adresu serveru pro připojení přes SFTP namísto `my.domain.com`.

## Prohlížeč logů

Pro zobrazení logů aplikace klikněte na tlačítko logů:

<center>
<img src="/img/apps-logs-button.png" class="shadow" width="600px">
</center>

Tím se otevře vyskakovací okno, které zobrazí logy:

<center>
<img src="/img/apps-logs.png" class="shadow" width="600px">
</center>

Logy jsou udržovány do velikosti 10 MB pro aktuální logy a jeden rotovaný log na aplikaci. Logy starší než 14 dní jsou odstraněny. Surové logy se nacházejí v `/home/yellowtent/platformdata/logs/<appid>/`.

## Grafy

Pohled na grafy ukazuje přehled využití CPU, disku, sítě a paměti aplikace.

<center>
<img src="/img/apps-graphs-memory.png" class="shadow" width="600px">
</center>

<center>
<img src="/img/apps-graphs-cpu.png" class="shadow" width="600px">
</center>

<center>
<img src="/img/apps-graphs-diskio.png" class="shadow" width="600px">
</center>

<center>
<img src="/img/apps-graphs-networkio.png" class="shadow" width="600px">
</center>

## Zastavení aplikace

Aplikaci lze zastavit pomocí tlačítka Stop v panelu nástrojů aplikace.

<center>
<img src="/img/app-stop-button.png" class="shadow" width="600px">
</center>

## Odinstalace


Odinstalováním aplikace, se okamžitě odstraní všechna data spojená s aplikací z OSCloud.

!!! note "Zálohy nejsou odstraněny"
    Zálohy aplikace nejsou při odinstalaci odstraněny a jsou vyčištěny pouze na základě zálohovací politiky. Aplikace mohou být vždy [obnoveny](/backups/#restoring-an-app-from-existing-backup) z jejich záloh pomocí nástroje CLI.

## Verze

S aplikací jsou spojeny dvě nezávislé verze. Tyto informace jsou uvedeny v sekci [Info](#info).

* `Verze balíčku`. OSCloud používá [semver](https://semver.org/) pro své balíčky aplikací.
* `Verze aplikace` nebo `Verze upstream`. Formát verzí aplikace se může výrazně lišit – může být založen na datech, semveru, číslech git commitů atd.
