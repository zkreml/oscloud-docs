# oscloud-docs

Tento repozitář obsahuje dokumentaci a návody pro platformu OSCloud, využívající MkDocs pro snadnou správu a nasazení.

## Přehled projektu

- **Účel:** Poskytnout podrobné návody a dokumentaci k používání a správě služeb OSCloud.
- **Technologie:** MkDocs – statický generátor stránek, který převádí soubory ve formátu Markdown na funkční a esteticky přehlednou webovou dokumentaci.

## Jak začít

1. **Klonování repozitáře:**
 ```bash
 git clone https://gitea.oscloud.cz/tvůj-uživatel/oscloud-docs.git
```

2. **Instalace MkDocs:**

```bash
pip install mkdocs
```
3. **Spuštění lokálně: Použij tento příkaz k spuštění MkDocs serveru a prohlížení dokumentace lokálně:**

```bash
mkdocs serve
```
4. **Vytvoření statických souborů: K vygenerování statických souborů pro nasazení:**

```bash
mkdocs build
```
## Nasazení na OSCloud pomocí LAMP

1. Přístup k LAMP serveru na OSCloud: Přihlas se do LAMP aplikace přes administraci na adrese `my.oscloud.cz` a otevři terminál pro danou aplikaci.

2. Instalace MkDocs na serveru: V terminálu na serveru spusť tento příkaz:

```bash
pip install mkdocs
```
3. *Vytvoření nového MkDocs projektu: Na serveru vytvoř nový projekt MkDocs pomocí tohoto příkazu:*

```bash
mkdocs new mysite
```
4. *Nahrání souborů: Nahrávej soubory projektu do kořenového adresáře LAMP aplikace pomocí FTP nebo SCP.*

5. *Spuštění MkDocs serveru: Na serveru spusť MkDocs příkazem:*

```bash
mkdocs serve
```
Dokumentace bude dostupná na veřejné URL, kterou LAMP aplikace poskytuje.

### Přispívání

Neváhejte nahlásit problémy nebo přispívat úpravami a vylepšeními do dokumentace prostřednictvím pull requestů.
