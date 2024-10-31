# <img src="/img/wordpress-managed-logo.png" width="25px"> WordPress (Spravovaná aplikace)

## O aplikaci

Tato aplikace je určena uživatelům, kteří chtějí spravovanou instalaci WordPressu. Tým OSCloud sleduje aktualizace WordPressu a publikuje aktualizace. Kód WordPressu je jen pro čtení, a proto je nutné WordPress rozšiřovat pomocí pluginů. Pokud potřebujete plnou kontrolu nad instalací, včetně úpravy kódu WordPressu, použijte [WordPress (nespravovaná aplikace)](/apps/wordpress-unmanaged).

* Dotazy? Zeptejte se v naší [Oscloud skupině na Mxchatu](https://matrix.to/#/!nnrBXdWbSiXkfiYtWR:mxchat.cz?via=mxchat.cz)

## Admin stránka

Admin stránka WordPressu je dostupná na `https://<mojedomena.cz>/wp-login.php`.

## Admin uživatel

Při použití WordPressu s OSCloud správou uživatelů je výchozí admin uživatel vytvořen s náhodným heslem a e-mailem `admin@cloudron.local`. Tento admin účet můžete po instalaci odstranit, pokud se přihlásíte jako správce. Není odstraněn automaticky, protože výchozí příspěvky generované instalátorem WordPressu jsou přiřazeny tomuto adminovi.

## Administrativní e-mailová adresa

WordPress používá administrativní e-mailovou adresu k odesílání důležitých e-mailů. Abyste tyto e-maily mohli přijímat, ujistěte se, že tuto adresu změníte v sekci `Nastavení`.

## Použití SFTP

Spravovaná aplikace WordPress nepodporuje úpravu souborů přes SFTP. Pokud potřebujete přístup SFTP pro úpravy souborů WordPressu, použijte [WordPress (vývojářská aplikace)](/apps/wordpress-developer).

## Limity paměti

Chcete-li nastavit paměť přidělenou pro WordPress, upravte soubor `/app/data/wp-config.php` pomocí [Správce souborů](/apps#file-manager) a přidejte následující řádky na konec souboru:

```php
define('WP_MEMORY_LIMIT', '128M'); define('WP_MAX_MEMORY_LIMIT', '256M');
```

Poznámka: Aplikace má také vlastní paměťový limit, který je řízen limitem aplikace. Pokud zvýšíte `WP_MEMORY_LIMIT`, ujistěte se, že také zvýšíte paměťový limit aplikace. Doporučený poměr je minimálně šestinásobek hodnoty `WP_MEMORY_LIMIT`.

## Úlohy Cron

Aplikace je nakonfigurována tak, aby spouštěla cron úlohy WordPressu každých 5 minut. Úlohy cron lze spustit ručně pomocí [webového terminálu](/apps#web-terminal):

```bash
wp cron event run --due-now
```


Vestavěný plánovač cron úloh WordPressu `wp-cron` je deaktivován, protože není efektivní pro weby s nízkou návštěvností.

## Pluginy

OSCloud nepodporuje pluginy, které upravují kód. Kód je pouze pro čtení a neměnný, což je nezbytné pro správné aktualizace aplikací na OSCloud. Pro pluginy, které upravují kód, použijte [WordPress (nespravovaná aplikace)](/apps/wordpress-unmanaged).

## Výkon

[GTmetrix](https://gtmetrix.com) je skvělá stránka pro získání metrik výkonu instalace WordPressu.

Pro nastavení hlaviček pro všechny stránky lze nainstalovat plugin [WP Fastest Cache](https://wordpress.org/plugins/wp-fastest-cache/).

## Přístup k databázi

OSCloud nepodporuje PHPMyAdmin. Přístup k databázi je však možný pomocí jiných metod:

* Otevřete [webový terminál](/apps#web-terminal) a spusťte konzoli MySQL.
* Použijte plugin jako [WP phpMyAdmin](https://wordpress.org/plugins/wp-phpmyadmin-extension/).

## WP CLI

[WP CLI](http://wp-cli.org/) je příkazový řádek pro WordPress. Pro spuštění příkazů CLI otevřete [webový terminál](/apps#web-terminal) a spusťte příkazy WP CLI. Například:

```bash
wp user list
```


## PHP nastavení

Můžete přidat vlastní [PHP nastavení](http://php.net/manual/en/ini.core.php) v `/app/data/htaccess` pomocí [Správce souborů](/apps#file-manager). 

Příklad:

```php
php_value post_max_size 600M
php_value upload_max_filesize 600
php_value memory_limit 128M
php_value max_execution_time 300
php_value max_input_time 300 
php_value session.gc_maxlifetime 1200
```


## Migrace existujícího webu

Podívejte se na náš [blog](https://blog.cloudron.io/migrating-a-wordpress-site-to-cloudron/) o tom, jak migrovat existující web WordPress na OSCloud.

## Úpravy souborů

Z bezpečnostních důvodů je vestavěná možnost úprav souborů ve WordPressu ve výchozím nastavení zakázána. 

Chcete-li ji povolit, upravte `/app/data/wp-config.php` a nastavte `DISALLOW_FILE_EDIT` na false.

```bash
define('DISALLOW_FILE_EDIT', false);
```
