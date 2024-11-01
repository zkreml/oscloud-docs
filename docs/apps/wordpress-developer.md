# <img src="/img/wordpress-developer-logo.png" width="25px"> WordPress (Vývojářská verze)

## O aplikaci

Tato aplikace je určena pro uživatele, kteří chtějí mít plnou kontrolu nad svou instalací WordPressu.

Funkce:

* Kód WordPressu lze upravovat. To znamená, že aktualizace WordPressu musíte spravovat sami pomocí vestavěného aktualizačního nástroje.
* Vlastní konfigurace Apache pomocí `.htaccess`
* Podpora [multisite](#multisite)

Pokud raději přenecháte odpovědnost za aplikaci aktualizací týmu Oscloud, použijte [Spravovanou aplikaci WordPress](/apps/wordpress-managed).

## Admin stránka

Admin stránka WordPressu se nachází na adrese `https://<moje.example.com>/wp-login.php`.

## Použití SFTP

Aplikaci lze nahrát pomocí SFTP klienta, jako je [FileZilla](https://filezilla-project.org/).

Přihlašovací údaje pro SFTP najdete po kliknutí na ikonu `i` v mřížce aplikací.

<center>
<img src="/img/lamp-filezilla.png" class="shadow" width="500px">
</center>

!!! poznámka "Přístup přes SFTP"
    Přístup přes SFTP pro uživatele bez administrátorských práv lze nastavit pomocí [rozhraní pro správu přístupu](/apps/#restricting-app-access-to-specific-users).

## Limity paměti

Pro úpravu paměti přidělené WordPressu upravte soubor `/app/data/wp-config.php` pomocí [správce souborů](/apps#file-manager)
a na konec souboru přidejte následující řádek:

```bash
define('WP_MEMORY_LIMIT', '128M'); define('WP_MAX_MEMORY_LIMIT', '256M');
```


Všimněte si, že aplikace má také samostatný paměťový limit, který lze nastavit prostřednictvím [limitu paměti aplikace](/apps/#increasing-the-memory-limit-of-an-app). Pokud zvýšíte `WP_MEMORY_LIMIT`, nezapomeňte také zvýšit limit paměti aplikace. Dobrou praxí je nastavit aplikaci minimálně 6násobek hodnoty `WP_MEMORY_LIMIT`.

`WP_MAX_MEMORY_LIMIT` je limit pro administrativní úlohy, které často vyžadují více paměti.

Podrobné vysvětlení najdete v [dokumentaci WordPressu](https://wordpress.org/support/article/editing-wp-config-php/#increasing-memory-allocated-to-php).

## Konfigurace Apache

Konfigurace Apache může být upravena pomocí mechanismu `htaccess`. Ve výchozím nastavení aplikace nemá soubor `.htaccess`. Tento soubor lze přidat pomocí [SFTP](/apps/wordpress-developer/#using-sftp) nebo [správce souborů](/apps#file-manager) v umístění `/app/data/public/.htaccess`. Stejně jako u jakékoli jiné standardní instalace Apache lze `.htaccess` přidat i do dalších podadresářů WordPressu v `/app/data/public/`, pokud je to potřeba.

## Cron úlohy

Aplikace je nastavena tak, aby spouštěla cron úlohy WordPressu každou minutu.

Pro ruční spuštění cron úloh použijte následující příkaz v
[webovém terminálu](/apps#web-terminal):

```bash
wp cron event run --due-now
```


Vestavěný plánovač úloh `wp-cron` je zakázán, protože je [neefektivní](https://www.lucasrolff.com/wordpress/why-wp-cron-sucks/) pro weby s nízkou návštěvností.

Pro přidání vlastních cron událostí použijte vestavěný [cron Oscloud](https://docs.cloudron.io/apps/#cron) nebo plugin, jako je [WP Crontrol](https://wordpress.org/plugins/wp-crontrol/).

## Pluginy

Na rozdíl od [spravované aplikace WordPress](/apps/wordpress-managed) můžete instalovat pluginy, které upravují kód.

### Deaktivace pluginu

Pokud některý plugin brání spuštění WordPressu, otevřete [správce souborů](/apps/#file-manager). Přejděte na
`/app/data/public/wp-content/plugins` a přejmenujte adresář s problémovým pluginem z `plugin-name` na například `plugin-name-broken`.

Pro opětovnou aktivaci pluginu je nutné nejen přejmenovat složku zpět, ale také plugin znovu aktivovat v administračním rozhraní WordPressu.

### Deaktivace všech pluginů

Pro deaktivaci všech pluginů přejmenujte `/app/data/public/wp-content/plugins` na `/app/data/public/wp-content/plugins-broken` pomocí
[správce souborů](/apps/#file-manager).

Pro opětovné povolení všech pluginů je nutné nejen přejmenovat složku zpět, ale také pluginy znovu aktivovat v administračním rozhraní WordPressu.

## Výkon

[GTmetrix](https://gtmetrix.com) je skvělý nástroj pro získání metrik výkonu instalace WordPressu.

* Pro nastavení vypršení záhlaví pro všechny stránky lze nainstalovat plugin [WP Fastest Cache](https://wordpress.org/plugins/wp-fastest-cache/).

* Pro CDN cache doporučujeme použít [WP Fastest Cache](https://wordpress.org/plugins/wp-fastest-cache/) nebo
[W3 Total Cache](https://wordpress.org/plugins/w3-total-cache/) pro cache na bázi CDN. Ryan Kite má
[dobrý návod](https://ryan-kite.com/how-to-create-a-cdn-for-wp-fastest-cache-with-aws-cloudfront/) na nastavení AWS Cloudfront s WP Fastest Cache.

## Přístup k databázi

Oscloud nepodporuje PHPMyAdmin. Přístup k databázi je však možný následujícími způsoby:

* Otevřete [webový terminál](/apps#web-terminal) a stiskněte tlačítko 'MySQL' pro přístup do konzole.
  Můžete přímo zadávat SQL příkazy.

* Použijte plugin jako [WP phpMyAdmin](https://wordpress.org/plugins/wp-phpmyadmin-extension/).


## WP CLI

[WP CLI](http://wp-cli.org/) je příkazová řádka pro WordPress. Pro spuštění příkazů
pomocí CLI nástroje otevřete [webový terminál](/apps#web-terminal) a
provádějte příkazy WP CLI jednoduše pomocí `wp`. Je již přednastaven tak, aby běžel jako správný uživatel.
Například:

```bash
wp user list
```

Pokud jeden nebo více pluginů/témat způsobuje chyby, můžete při spuštění WP CLI přeskočit načítání pluginů/témat pomocí:

```
wp --skip-plugins --skip-themes
```


Další nastavení PHP lze konfigurovat při ručním spuštění s `php -d key=value`:
```bash
sudo -E -u www-data php -d max_execution_time=100 /app/pkg/wp --path=/app/data/public/
```


V tomto případě se maximální doba vykonávání nastaví na 100 sekund.

## Nastavení PHP

Vlastní [nastavení PHP](http://php.net/manual/en/ini.core.php) můžete přidat do souboru `/app/data/php.ini`

### Velikost nahrávaných souborů

Upravte následující hodnoty v souboru `/app/data/php.ini`:

```php
post_max_size = 256M 
upload_max_filesize = 256M 
memory_limit = 256M
```


## Migrace existujícího webu

Podívejte se na náš [blog](https://blog.cloudron.io/migrating-a-wordpress-site-to-cloudron/) ohledně migrace
existujícího WordPress webu na Oscloud.

## Úprava souborů

Vestavěná funkce pro úpravu souborů WordPressu je ve výchozím nastavení povolena. Z bezpečnostních důvodů doporučujeme
tuto možnost vypnout, a to úpravou souboru `/app/data/wp-config.php` a nastavením `DISALLOW_FILE_EDIT` na hodnotu true.

```bash
define('DISALLOW_FILE_EDIT', true);
```


## Email

Ve výchozím nastavení je aplikace nakonfigurována tak, aby používala plugin [smtp-mailer](https://wordpress.org/plugins/smtp-mailer/).

Vlastní plugin pro odesílání emailů lze použít následovně:

* [Zakázat konfiguraci emailu](/apps/#disable-email-configuration) v App -> Email -> `Nepoužívat nastavení emailu aplikace`. Pokud je zakázáno, Oscloud nebude při každém restartu konfigurovat `smtp-mailer`.

<center>
<img src="/img/wordpress-mailbox-disable.png" class="shadow" width="90%">
</center>

* Nainstalujte preferovaný plugin pro odesílání emailů ve WordPressu.

* Přihlašovací údaje k emailu závisí na vaší konfiguraci. Pokud používáte externí poštovní službu, jako je Mailgun/SES/Postmark, můžete tyto údaje použít přímo ve WordPressu. Alternativně si můžete vytvořit přihlašovací údaje pro relay nebo poštovní schránku u vašeho poskytovatele emailu.

* Pokud používáte Oscloud jako svůj emailový server, jednoduše vytvořte poštovní schránku a použijte [heslo k aplikaci](/profile/#app-passwords). Jako odesílací server použijte konfiguraci [SMTP](/email/#smtp) serveru. Pro větší bezpečnost můžete zvážit vytvoření samostatného uživatele Oscloud, který bude vlastnit vytvořenou poštovní schránku (tím se zabrání tomu, aby mohl špatný plugin přistupovat k vašim osobním schránkám). Upozorňujeme, že uživatelské jméno SMTP je stejné jako adresa poštovní schránky (nikoli uživatelské jméno Oscloud).

<center>
<img src="/img/wordpress-email-app-password.png" class="shadow" width="500px">
</center>

Konfigurace pluginu Fluent SMTP:

<center>
<img src="/img/wordpress-fluent-smtp.png" class="shadow" width="500px">
</center>

## Neomezený HTML

Ne-admin uživatelům je povoleno vkládat neomezený HTML obsah. Tuto možnost lze zakázat úpravou
souboru `/app/data/wp-config.php` a nastavením `DISALLOW_UNFILTERED_HTML` na hodnotu true.

```
define('DISALLOW_UNFILTERED_HTML', true);
```


## Multisite


!!! poznámka "Použít nebo nepoužít multisite"
    WordPress multisite je složitý systém s mnoha problémy kompatibility. Pokud nemáte zásadní důvod, doporučujeme
    instalovat samostatnou aplikaci WordPress pro každou stránku.

Pro aktivaci WordPress multisite začněte s novou instalací a použijte nástroj pro nastavení sítě (Network Setup Tool).

* Aktivujte multisite v souboru `/app/data/public/wp-config.php` přidáním následujícího řádku pomocí [správce souborů](/apps/#file-manager).
  Tento řádek vložte nad text "That’s all, stop editing! Happy blogging.":

```bash
/* Multisite */ define( 'WP_ALLOW_MULTISITE', true );
```


* V administračním rozhraní WordPressu přejděte do `Nástroje` -> `Nastavení sítě`. Podle pokynů na této stránce deaktivujte všechny pluginy před pokračováním. Oscloud podporuje instalaci jak na subdoménách, tak v podadresářích.

<center>
<img src="/img/wordpress-tools-network-setup.png" class="shadow" width="500px">
</center>

* Po kliknutí na instalaci se zobrazí zpráva `Upozornění! Wildcard DNS možná není správně nakonfigurováno!`. Pro opravu přejděte do
  zobrazení `Umístění` na Oscloud dashboardu a nastavte alias s hvězdičkou (Wildcard alias). Jakmile je alias přidán, upozornění zmizí
  (obnovte administrační rozhraní WordPressu).

<center>
<img src="/img/wordpress-multisite-alias.png" class="shadow" width="500px">
</center>

* Pro dokončení instalace sítě přidejte do `/app/data/public/wp-config.php` následující řádky podle pokynů.

```
define('MULTISITE', true);
define('SUBDOMAIN_INSTALL', true);
define('DOMAIN_CURRENT_SITE', 'msite.cloudron.club');
define('PATH_CURRENT_SITE', '/');
define('SITE_ID_CURRENT_SITE', 1);
define('BLOG_ID_CURRENT_SITE', 1);
```


Dále kompletně nahraďte obsah souboru `/app/data/public/.htaccess` podle pokynů. Upozorňujeme, že pravidla přepisování (Rewrite rules) se mírně liší pro instalaci na subdoménách a v podadresářích. Následující konfigurace je pro nastavení na subdoménách:


```bash
RewriteEngine On
RewriteRule .* - [E=HTTP_AUTHORIZATION:%{HTTP:Authorization}]
RewriteBase /
RewriteRule ^index\.php$ - [L]

# add a trailing slash to /wp-admin
RewriteRule ^wp-admin$ wp-admin/ [R=301,L]

RewriteCond %{REQUEST_FILENAME} -f [OR]
RewriteCond %{REQUEST_FILENAME} -d
RewriteRule ^ - [L]
RewriteRule ^(wp-(content|admin|includes).*) $1 [L]
RewriteRule ^(.*\.php)$ $1 [L]
RewriteRule . index.php [L]
```
* Nové stránky můžete přidávat z nabídky `Správce sítě`. Stránku můžete přidat jako subdoménu nebo podadresář. Adresu stránky lze po přidání upravit v nastavení stránky.

* Pokud nastavíte adresu stránky na jinou doménu, stačí ji přidat do aliasů domény v sekci `Umístění` na Oscloud Dashboardu.

<center>
<img src="/img/wordpress-multisite-new-site.png" class="shadow" width="500px">
</center>

### Nastavení emailu (Multisite)

V režimu multisite lze plugin pro SMTP odesílání nastavit pro každou stránku zvlášť. Po přidání nové stránky restartujte aplikaci, aby se plugin automaticky nakonfiguroval v kódu balíčku.