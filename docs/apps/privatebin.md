# <img src="/img/privatebin-logo.png" width="25px"> PrivateBin App

## Co je PrivateBin?

PrivateBin je minimalistická, open-source aplikace, která umožňuje bezpečné sdílení textových zpráv, souborů nebo poznámek. PrivateBin je zaměřený na soukromí a bezpečnost a využívá end-to-end šifrování (E2EE), což znamená, že obsah, který sdílíte, je šifrován přímo ve vašem prohlížeči a dešifrován pouze příjemcem. Server nemá žádný přístup k obsahu, protože uložená data jsou šifrována na straně klienta.

<center>
<img src="/img/privatebin_app.png" class="shadow" width="500px">
</center>


## Výhody PrivateBin

- End-to-End Šifrování: Všechna data jsou šifrována lokálně, což znamená, že ani provozovatel serveru nemůže vidět obsah poznámek.
- Samodestrukční poznámky: Můžete nastavit časový limit pro poznámku, po kterém bude automaticky smazána.
- Ochrana heslem: Můžete ke sdílené poznámce přidat heslo, čímž zvýšíte její bezpečnost.
- Podpora pro MIME typy: PrivateBin podporuje různé typy textového obsahu včetně prostého textu, markdownu, kódu nebo souborů.
- Diskrétnost: PrivateBin neukládá žádné uživatelské informace, jako jsou IP adresy, a nevyžaduje žádnou registraci.

## Jak PrivateBin funguje

PrivateBin využívá moderní šifrovací technologie, aby zajistil, že obsah je přístupný pouze odesílateli a příjemci. Každá poznámka, která je odeslána prostřednictvím PrivateBin, je nejprve zašifrována v prohlížeči odesílatele pomocí 256bitového AES šifrování a následně odeslána na server.

- Uživatel vytvoří poznámku: Do webového rozhraní PrivateBin vloží text nebo soubor.
- Zašifrování: Poznámka je šifrována v prohlížeči pomocí klíče, který je následně připojen k URL.
- Sdílení: Uživatel sdílí URL s příjemcem. Server nemá přístup ke klíči, který je uložen v URL.
- Dešifrování: Příjemce otevře URL, která obsahuje klíč. Poznámka je dešifrována v prohlížeči příjemce.

## Použijte naší instanci [Privatebin](https://privatebin.arch-linux.cz)

Naše instance PrivateBin je k dispozici na [adrese](https://privatebin.arch-linux.cz). Je plně šifrovaná a umožňuje vám sdílet bezpečné poznámky a soubory. Služba je nastavena tak, aby maximálně respektovala vaše soukromí.
Příklady použití PrivateBin

- Sdílení citlivých informací: PrivateBin je ideální pro sdílení citlivých informací, jako jsou hesla, API klíče nebo důležité poznámky.
- Dočasné poznámky: Můžete sdílet poznámky, které se samy zničí po jejich přečtení, což zajišťuje, že nezůstanou uloženy na serveru.
- Spolupráce na kódu: PrivateBin podporuje zvýraznění syntaxe, takže je vhodný i pro sdílení úryvků kódu mezi vývojáři.

## Zabezpečení a ochrana soukromí

PrivateBin byl navržen s ohledem na maximální zabezpečení. Díky end-to-end šifrování není obsah dešifrován, dokud není příjemcem otevřen. Navíc server neukládá IP adresy uživatelů, což znamená, že neexistuje žádná vazba mezi uživatelem a poznámkou.

Je důležité zdůraznit, že i když PrivateBin nabízí silné zabezpečení, uživatelé by měli být opatrní při sdílení odkazů a volbě silných hesel pro dodatečnou ochranu.
## Závěr

PrivateBin je jednoduchý, ale účinný nástroj pro zabezpečené sdílení informací. Díky end-to-end šifrování a možnosti nastavení dočasných poznámek se stává ideálním řešením pro všechny, kdo potřebují bezpečně sdílet obsah. Pokud hledáte snadno nasaditelnou a soukromou platformu pro sdílení dat, PrivateBin je skvělá volba.

Navštivte naši instanci [Privatebin](https://privatebin.arch-linux.cz) a začněte bezpečně sdílet poznámky ještě dnes.