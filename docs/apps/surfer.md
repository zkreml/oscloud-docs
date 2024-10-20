# <img src="/img/surfer-logo.png" width="25px"> Surfer App


### Surfer na OSCloud

Surfer je aplikace pro snadnou správu souborů a hosting statických webových stránek na OSCloud. Je ideální pro rychlé nasazení webových projektů, dokumentací nebo jednoduchých webových aplikací.



### 1. Přístup k Surferu
Přihlašte se do administrace OSCloud a zvolte aplikaci Surfer z katalogu aplikací. Instalaci provádíme za zákazníka a aplikace bude po dokončení automaticky dostupná na subdoméně zákazníka, například `firmy.oscloud.cz`.

### 2. Přístup k souborům

Jakmile je aplikace Surfer nainstalovaná, získá zákazník přístup ke správě souborů prostřednictvím jednoduchého webového rozhraní. Toto rozhraní umožňuje nahrávat, stahovat, mazat a organizovat soubory na jeho subdoméně. Případné úpravy a asistenci s nahráváním prvních souborů zajišťujeme také my, aby zákazník nemusel mít technické znalosti k obsluze aplikace.


### 3. Další možnosti správy souborů

Existují 4 způsoby, jak spravovat soubory v aplikaci Surfer:

* [Webové rozhraní](#webové-rozhraní)
* [CLI nástroj](#cli-nástroj)
* [WebDAV](#webdav) endpoint pro správu souborů ve vašem lokálním správci souborů.
* [SFTP](#sftp)

#### Webové rozhraní

Soubory můžete nahrávat a spravovat přes webové rozhraní na adrese `https://[vaše-doména]/_admin`. Zde můžete také spravovat strukturu složek a jednotlivé soubory.

<center>
<img src="/img/surfer-web-interface.png" class="shadow" width="500px">
</center>


#### CLI nástroj

Pokud preferujete práci z příkazového řádku, můžete využít CLI nástroj pro Surfer. Nejprve ho nainstalujte pomocí npm:

```bash
npm -g install cloudron-surfer
```

Přihlaste se pomocí přístupového tokenu vytvořeného v administraci Surferu:

```bash
surfer config --server <doména-aplikace> --token
```

Nahrajte soubory:

```bash
surfer put index.html favicon.ico /
```

Nahrajte adresář (příkaz `/*` znamená, že obsah adresáře `build` bude zkopírován do kořenového adresáře Surferu):

```bash
surfer put build/* /
```
Získání nápovědy:

```bash
$ surfer
Usage: surfer [options] [command]

Options:
  -V, --version                output the version number
  -h, --help                   display help for command

Commands:
  login                        Set default server
  logout                       Unset default server
  config|configure [options]   Configure default server
  put [options] <file|dir...>  Uploads a list of files or dirs to the destination. The last argument is destination dir
  get [options] [file|dir]     Get a file or directory listing
  del [options] <file>         Delete a file or directory
  help [command]               display help for command

```
### WebDAV

[WebDAV](https://en.wikipedia.org/wiki/WebDAV)  je rozšíření HTTP protokolu, které umožňuje vzdálenou správu souborů. WebDAV sdílení můžete připojit pomocí vašeho správce souborů.

URI schémata se liší na běžných platformách.

| Platform| URI |
| ---     | --- |
| Windows | `https://[appdomain]/_webdav/` |
| Mac     | `https://[appdomain]/_webdav/` |
| Gnome   | `davs://[appdomain]/_webdav/` |
| KDE     | `webdavs://[appdomain]/_webdav/` |


!!! note "Přístup přes WebDAV" Pro přístup přes WebDAV použijte přístupový token vytvořený v administraci Surferu jako heslo.

Na Linuxu můžete použít knihovnu [Davfs2](http://savannah.nongnu.org/projects/davfs2) pro lokální připojení sdílené složky:

```bash
mount -t davfs https://[doména-aplikace]/_webdav/ /mnt/bod
```

### SFTP

Soubory lze nahrávat pomocí SFTP klienta jako je [FileZilla](https://filezilla-project.org/). Podrobnosti o [SFTP přístupu](/apps/#sftp-access) najdete v administraci aplikace.

!!! note "Přístup přes SFTP" Přístup přes SFTP pro uživatele bez administrátorských práv lze udělit prostřednictvím rozhraní pro správ

### Ovládání přístupu

Přístup na stránky lze řídit prostřednictvím stránky Nastavení. K dispozici jsou tři možnosti:

- Veřejný přístup (pro všechny) – kdokoli může web zobrazit.
- Přístup omezený heslem – kdokoli s heslem může web zobrazit.
- Omezený přístup pro uživatele – pouze uživatelé s přihlášením na OSCloud mohou web zobrazit.

<center>
<img src="/img/surfer-access-control.png" class="shadow" width="500px">
</center>




### CI/CD integrace

Můžete nastavit svůj CI/CD systém tak, aby automaticky nahrával statické soubory do aplikace Surfer pomocí CLI nástroje následujícím způsobem:

- Nejprve vytvořte Access Token v aplikaci Surfer z nabídky Nastavení.

- Nainstalujte CLI nástroj Surfer jako součást CI/CD pipeline.

- Nahrajte artefakty (v níže uvedeném příkladu složku dist/):

```bash
surfer put --token api-7e6d90ff-5825-4ebe-a85b-a68795055955 --server surfer.oscloud.cz dist/* /
```