# <img src="/img/trilium-logo.png" width="25px"> Trilium Next

Hledáš nástroj na poznámky, který ti nenechá data v cloudu nějaké korporace? Potřebuješ něco víc než jen textový editor, ale nechceš platit měsíční předplatné? Trilium Next je open-source aplikace na správu poznámek a znalostní báze, kterou si nasadíš sám a máš plnou kontrolu.

<center>
<img src="/img/trilium1.png" class="shadow" width="500px">
</center>

## Co je Trilium Next?

Trilium Next je fork původního projektu Trilium Notes, který pokračuje ve vývoji poté, co byl původní projekt ukončen. Jde o webovou aplikaci s desktopovým klientem, která ti umožní vytvořit hierarchickou strukturu poznámek s pokročilými funkcemi jako šifrování, verzování, grafy vztahů a mnoho dalšího.

Hlavní filosofie? **Tvoje data, tvůj server, tvoje kontrola.**

## Klíčové vlastnosti

### Hierarchie a flexibilní struktura

Na rozdíl od lineárních poznámek máš v Trilium stromovou strukturu - poznámky můžeš vnořovat do sebe, vytvářet větve a organizovat je podle toho, jak ti to dává smysl. Jedna poznámka může být na více místech najednou pomocí klonování.

### Šifrování na úrovni poznámek

Můžeš označit jednotlivé poznámky jako "protected" a ty se pak šifrují pomocí hesla. Šifrování běží na straně klienta, takže ani při synchronizaci přes server nemá nikdo jiný přístup k obsahu. Používá se AES-128 v CBC módu.

### Verzování a historie změn

Každá změna poznámky se automaticky verzuje. Můžeš se vrátit k libovolné starší verzi, porovnat změny nebo obnovit smazaný obsah. Historie je kompletní a nic se neztrácí.

### Grafy a vztahy

Trilium ti umožňuje vytvářet vztahy mezi poznámkami (linky, ale i atributy) a zobrazovat je jako graf. Vidíš propojení svých myšlenek a můžeš procházet souvislosti mezi tématy.

<center>
<img src="/img/trilium3.png" class="shadow" width="500px">
</center>

<center>
<img src="/img/trilium4.png" class="shadow" width="500px">
</center>

### Skripty a automatizace

Podporuje JavaScript skripty – můžeš si psát vlastní funkce, automaty na zpracování poznámek, widgety do rozhraní nebo dokonce celé mini-aplikace uvnitř Trilia.

### Markdown, kód, tabulky, obrázky

- Markdown s živým náhledem (live preview)
- Zvýraznění syntaxe (Syntax highlighting) pro desítky jazyků
- Tabulky s možností editace
- Vkládání obrázků, PDF, přílohy
- Diagramy (Mermaid, Excalidraw)
- Matematické vzorce (KaTeX)

<center>
<img src="/img/trilium5.png" class="shadow" width="500px">
</center>

<center>
<img src="/img/trilium2.png" class="shadow" width="500px">
</center>

### Full-text vyhledávání

Prohledává všechny poznámky včetně atributů, kódu a příloh. Vyhledávání je rychlé i na tisících poznámek.

## Bezpečnost a soukromí

### Self-hosted = plná kontrola

Protože běží na našem serveru nebo na tvém počítači, máš nad Triliem plnou kontrolu. Bez vendor lock-inu, bez třetích stran, bez nejasných cloudových služeb.

### End-to-end šifrování chráněných poznámek

Když poznámku označíš jako "protected":

- Šifruje se lokálně před odesláním na server
- Dešifruje se až po zadání hesla v klientovi
- Na serveru leží pouze šifrovaná data
- Nikdo bez hesla k nim nemá přístup

### HTTPS a přístupová hesla

Trilium podporuje basic auth i vlastní přihlašovací systém. Pokud ho zpřístupníš přes internet, rozhodně to dělej přes HTTPS (Nginx/Caddy reverse proxy).

### Žádná telemetrie, žádné trackování

Open source projekt bez analytiky, bez reportování "domů", bez sledování. Co děláš v Triliu zůstává v Triliu.

### Pravidelné zálohy

Můžeš si nastavit automatické exporty celé databáze. Trilium ukládá vše do SQLite databáze, takže stačí zálohovat jeden soubor.

## Synchronizace mezi zařízeními

Trilium má vestavěný sync server. Sync funguje obousměrně, řeší konflikty a zachovává šifrování chráněných poznámek.

## Proč Trilium Next místo alternativ?

### Vs Notion, Obsidian

- **Notion**: Proprietární cloud, nemáš přístup k datům, vendor lock-in
- **Obsidian**: Sice lokální soubory, ale uzavřený kód,
- **Trilium Next**: Open source, self-hosted, zdarma, bez omezení

### Vs Joplin, Standard Notes

- **Joplin**: Dobrá alternativa, ale méně pokročilé funkce (grafy, skripty)
- **Standard Notes**: Minimalističtější, méně zaměřená na znalostní bázi
- **Trilium Next**: Komplexní nástroj s pokročilými funkcemi pro power usery

### Vs klasické wiki (MediaWiki, BookStack)

- Wiki systémy jsou těžší na správu a často pomalejší
- Trilium je jednodušší na nasazení a rychlejší v používání
- Lepší UX pro osobní poznámky a hierarchii

## Pro koho je Trilium Next?

### Pro běžné uživatele

I když Trilium vypadá jako technický nástroj, klidně ho může používat každý. Nemusíš rozumět kódu nebo serverům – stačí si stáhnout desktop aplikaci a máš hotovo.

**Co ti Trilium dá jako běžnému uživateli:**

- **Osobní deník/žurnál**: Piš si denně poznámky, myšlenky, plány. Vše pěkně seřazené podle data, snadno vyhledatelné
- **Recepty a kuchařka**: Vlastní databáze receptů s fotkami, ingrediencemi a poznámkami. Žádné reklamy, žádné souhlas s cookies
- **Cestovní plány**: Itineráře, rezervace, poznámky z cest. Vše na jednom místě, offline dostupné
- **Nápady a projekty**: Renovace baráku, nápady na zahradu, plány na víkend. Můžeš k nim přidávat odkazy, obrázky, checklisty
- **Učení se novým věcem**: Poznámky z kurzů, tutoriálů, knížek. Propojuj témata a vytvářej si vlastní wiki
- **Finanční přehled**: Rozpočty, výdaje, investice. Můžeš si udělat vlastní tabulky a grafy

**Proč ne Google Keep, Evernote nebo OneNote?**

- Nevyžaduje internet (pokud nechceš sync)
- Nic se ti nepřestane fungovat, když přestanou službu podporovat
- Nedostáváš reklamy na prémiové funkce
- Nikdo ti nečte poznámky kvůli cílení reklam
- Neplatíš měsíční poplatek za víc GB

### Pro pokročilé uživatele

- **Programátoři**: ukládání snippetů, dokumentace projektů, technical notes
- **Studenti**: organizace poznámek, výpisků, propojování témat
- **Výzkumníci**: správa vědomostí, citace, grafy souvislostí
- **Privacy enthusiasté**: žádné cloudy, vše pod kontrolou
- **Sysadmini**: dokumentace serverů, postupy, runbooky

## Technické info

- **Backend**: Node.js + SQLite
- **Frontend**: JavaScript (desktop klient je Electron)
- **Licence**: AGPL-3.0
- **Platformy**: Linux, Windows, macOS, web
- **Mobilní**: Community app (TriliumNext Notes pro Android)

## Závěr

Trilium Next je mocný nástroj pro každého, kdo chce mít svou znalostní bázi pod kontrolou. Není to jen "další Notion" – je to plnohodnotný systém pro správu poznámek s důrazem na soukromí, bezpečnost a otevřenost.

Pokud ti vadí závislost na komerčních službách, a máš rád open source, určitě mu dej šanci.

## Technické info

* **Backend**: Node.js + SQLite
* **Frontend**: JavaScript (desktop klient je Electron)
* **Licence**: AGPL-3.0
* **Platformy**: Linux, Windows, macOS, web
* **Mobilní**: Community app (Trilium Next Notes pro Android)

## Trilium Next na OSCloud

Na OSCloud nabízíme Trilium Next jako **prémiovou aplikaci** pouze pro vážné zájemce. Pokud víš, že Trilium je přesně to, co hledáš, můžeš si u nás zažádat o vlastní instanci.

### Co nabízíme:

* ✅ Vlastní subdoména ve tvaru `jmeno.oscloud.cz` nebo vlastní doména
* ✅ Oddělená instance – tvoje data, tvoje prostředí
* ✅ Pravidelné zálohy a HTTPS zabezpečení
* ✅ Přístup přes webové rozhraní i synchronizaci s desktop klientem

### Jak požádat o přístup?

1. Napiš nám přes [helpdesk.oscloud.cz](https://helpdesk.oscloud.cz/help/711028727)
2. Uveď:

   * Požadovanou subdoménu (např. `poznámky.oscloud.cz`)
   * Jak plánuješ Trilium používat (dobrovolné)
3. Po schválení ti připravíme instanci a zašleme přístupy

> Trilium nenabízíme plošně – chceme, aby jej využívali lidé, kteří s ním vědomě pracují a mají zájem o dlouhodobé použití.

## Ceník Trilium Next na OSCloud

| Plán                     | Cena             | Popis |
|--------------------------|------------------|-------|
| **Základní**             | 65 Kč / měsíc    | Vlastní instance Trilium Next, přístup odkudkoli |
| **Roční**                | 600 Kč / rok     | Zvýhodněná cena|
| **Vlastní doména** *(volitelné)* | individuálně | Podpora vlastní domény (např. poznámky.mojedomena.cz) na vyžádání |

💾 Neexistuje tvrdý limit na velikost dat, ale prosíme:  
pokud plánuješ nahrávat velké množství videí, PDF nebo jiných velkých souborů, dej nám předem vědět.  
Chceme zachovat férové sdílení prostředků mezi všemi uživateli.

📦 V základním plánu počítáme s typickým textovým použitím – poznámky, přílohy do stovek MB.  
Pokud budeš potřebovat více, rádi se domluvíme individuálně.

## Chceš si Trilium Next nejdřív vyzkoušet?

Nabízíme možnost **demo instance zdarma** po dobu několika dní. Můžeš si vyzkoušet prostředí, funkce a rozhodnout se, jestli ti Trilium vyhovuje.

Stačí napsat žádost přes náš [helpdesk](https://helpdesk.oscloud.cz/help/711028727) nebo e-mailem na [podpora@oscloud.cz](mailto:podpora@oscloud.cz) a my ti demo co nejdříve zřídíme.


---

**Odkazy:**

* GitHub: [https://github.com/TriliumNext/Trilium](https://github.com/TriliumNext/Trilium)
* Dokumentace: [https://triliumnotes.org/](https://triliumnotes.org/)
* Demo: Můžeš si ho vyzkoušet lokálně bez instalace
