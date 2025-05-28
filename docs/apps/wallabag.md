# <img src="/img/wallabag-logo.png" width="25px"> Wallabag na Oscloud

Wallabag je open-source aplikace určená pro ukládání, organizaci a čtení článků. Umožňuje vám ukládat obsah webových stránek, odstranit rušivé prvky, jako jsou reklamy, a číst články v jednoduchém formátu.

<center>
<img src="/img/wallabag_app.png" class="shadow" width="500px">
</center>


Na OSCloud je Wallabag dostupný na adrese [read.oscloud.cz](https://read.oscloud.cz/). Pro registraci je nutné kontaktovat podporu na [helpdesk.oscloud.cz](https://helpdesk.oscloud.cz/help/3020290644) nebo emailem na [podpora@oscloud.cz](mailto:podpora@oscloud.cz).

## Srovnání se službami Pocket, Instapaper a Wallabag

| Funkce                      | Wallabag     | Pocket      | Instapaper |
|-----------------------------|--------------|-------------|------------|
| Open-source                 | Ano          | Ne          | Ne         |
| Šifrování dat               | Částečně[^1] | Ne          | Ne         |
| Offline přístup             | Ano          | Ano         | Ano        |
| Přizpůsobitelné rozhraní    | Ano          | Ne          | Částečně   |
| Ukládání bez reklam         | Ano          | Ano         | Ano        |
| Import/export dat           | Ano          | Ano         | Ano        |
| Podpora více uživatelů      | Ano          | Ne          | Ne         |

[^1]: Wallabag podporuje šifrování dat během přenosu pomocí HTTPS. Data uložená na serveru však nejsou automaticky šifrována end-to-end.

## Bezpečnost

- **Kontrola nad daty**: Protože je Wallabag open-source, můžete si být jisti, že vaše data nejsou sledována třetími stranami. Aplikaci můžete provozovat na vlastním serveru nebo využít OSCloud.
- **Soukromí**: Vaše data nejsou sdílena s žádnou reklamní sítí.
- **HTTPS**: Wallabag na OSCloud využívá HTTPS pro zabezpečení přenosu dat.

## Výhody Wallabag

1. **Jednoduchost**: Články můžete číst bez rušivých prvků, jako jsou reklamy nebo nepotřebné prvky stránky.
2. **Organizace**: Umožňuje štítkovat články a organizovat je podle kategorií.
3. **Export dat**: Možnost exportovat své uložené články ve formátu HTML, JSON nebo EPUB.
4. **Podpora aplikací**: K dispozici jsou mobilní aplikace pro Android a iOS.

## Mobilní aplikace Wallabag

Pro pohodlný přístup na cestách si stáhněte mobilní aplikaci Wallabag:

[![Google Play](https://upload.wikimedia.org/wikipedia/commons/7/78/Google_Play_Store_badge_EN.svg)](https://play.google.com/store/apps/details?id=fr.gaulupeau.apps.InThePoche)
[![App Store](https://developer.apple.com/assets/elements/badges/download-on-the-app-store.svg)](https://apps.apple.com/us/app/wallabag/id1170800946)


Po instalaci aplikace propojte svůj účet Wallabag na OSCloud podle přiložených pokynů v aplikaci.

## Jak začít

1. Požádejte o registraci přes [Objednávky Oscloud](https://helpdesk.oscloud.cz/help/3020290644).
2. Po schválení registrace obdržíte přihlašovací údaje.
3. Přihlaste se na [read.oscloud.cz](https://read.oscloud.cz/) pomocí poskytnutých údajů.
4. Nainstalujte si mobilní aplikaci Wallabag.
5. Propojte aplikaci s vaším OSCloud účtem.

## Další informace

Pro více informací o funkcích Wallabag navštivte [oficiální web Wallabag](https://wallabag.org/).

Na Oscloudu můžeš ve Wallabagu ukládat a číst články z českých zpravodajských webů. Některé z nich fungují i za přihlášením (např. Deník N).

---

## ✅ České weby, které aktuálně fungují

Tyto domény mají podporu ve Wallabagu a měly by správně fungovat:

-  `denikn.cz` *(funguje i s paywallem – viz níže)*
-  `novinky.cz`
-  `root.cz`
-  `lupa.cz`
-  `zdopravy.cz`
-  `seznamzpravy.cz`
-  `reportermagazin.cz`

---

## 🔐 Jak číst Deník N

1. Klikni na **Site credentials** (ikona klíče vpravo nahoře)
2. Zadej přihlašovací údaje k Deníku N:
   - **Host:** `denikn.cz`
   - **Login:** e-mail
   - **Password:** heslo
3. Ulož. Hotovo.

<center>
<img src="/img/denik_walabag1.png" class="shadow" width="400px">
</center>

<center>
<img src="/img/denik_walabag2.png" class="shadow" width="400px">
</center>

Nyní můžeš vkládat odkazy na články z Deníku N, a pokud máš předplatné, Wallabag je zobrazí.

## 🦊 Wallabag – přidání rozšíření do Firefoxu

Tento návod ti ukáže, jak do Firefoxu přidat rozšíření **Wallabagger**, propojit ho se svým účtem ve Wallabagu (např. na OSCloudu) a začít si ukládat články jedním kliknutím.

---

## 📹 Videonávod

<iframe title="Jak přidat Wallabag rozšíření do Firefoxu"
        width="100%"
        height="400"
        src="https://vhsky.cz/videos/embed/tmrCgnyzXFQnyamxLyFpJr"
        frameborder="0"
        allowfullscreen
        sandbox="allow-same-origin allow-scripts allow-popups allow-forms">
</iframe>

> *Toto video ukazuje celý postup krok za krokem.*

---

## 🔧 Podrobný postup

### 1. Nainstaluj rozšíření Wallabagger

1. Otevři Firefox
2. Přejdi na stránku doplňku:  
   👉 [Wallabagger na Mozilla Add-ons](https://addons.mozilla.org/cs/firefox/addon/wallabagger/)
3. Klikni na **Přidat do Firefoxu** a potvrď instalaci

Po instalaci se vpravo nahoře objeví ikonka slona (🐘).

---

### 2. Přihlas se do Wallabag a vytvoř API klienta

1. Otevři svou instanci [Wallabag](https://read.oscloud.cz/)
2. Přejdi do: **Nastavení → Správa API klientů**
3. Klikni na **Přidat klienta**
4. Vyplň:
   - **Název**: např. „Firefox“
5. Ulož si **Client ID** a **Client Secret**

---

### 3. Nastav rozšíření ve Firefoxu

1. Klikni na ikonku Wallabaggeru (vpravo nahoře)
2. V poli nastavení vyplň:
   - **Wallabag instance URL**: `https://read.oscloud.cz`
   - **Client ID**: z kroku 2
   - **Client Secret**: z kroku 2
3. Jméno uživatele a heslo


---

## ✅ Hotovo!

Teď můžeš:
- jedním klikem ukládat články do Wallabag
- číst je později bez reklam a sledování
- používat rozšíření i na mobilu (přes Firefox + přihlášení)


## Další informace

Pro více informací o funkcích Wallabag navštivte [oficiální web Wallabag](https://wallabag.org/).

