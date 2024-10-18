# <img src="/img/lamp-logo.png" width="25px"> LAMP Aplikace

## O aplikaci

Provozování LAMP aplikací na OSCloud není odlišné od toho, co je dostupné na mnoha hostingových poskytovatelích. Svůj PHP kód můžete nahrát pomocí SFTP nebo pomocí [Správce souborů](/apps#file-manager) a následně upravit soubory `.htaccess` a `php.ini` dle potřeby. Většina běžně používaných [PHP rozšíření](#php-rozšíření) je předinstalována a nemusíte se starat o jejich aktualizaci.

Hlavní výhody používání OSCloud k hostování LAMP aplikací jsou:

* Automatická konfigurace DNS, instalace a obnova SSL certifikátů Let's Encrypt.
* Možnost využívat MySQL, Redis a odesílat e-maily.
* Nemusíte se starat o zálohy aplikací a serveru, obnovení a aktualizace, protože o to se stará OSCloud.
* Provoz více LAMP aplikací, izolovaných od sebe, na stejném serveru.

## Podporované verze PHP

Aplikace LAMP podporuje následující verze PHP:

* 7.4
* 8.0
* 8.1
* 8.2
* 8.3 (výchozí)

Chcete-li změnit verzi PHP, upravte soubor `/app/data/PHP_VERSION` pomocí [Správce souborů](/apps/#file-manager) a restartujte aplikaci.

!!! warning "PHP CLI"
    Binární soubor `php` je pevně nastaven na používání PHP 8.3. V případě skriptů použijte explicitně `php8.0`, `phar8.0` a podobně.

## Nahrávání souborů

Soubory LAMP aplikace lze nahrát pomocí [Správce souborů](/apps/#file-manager) nebo SFTP.

### SFTP

Aplikace může být nahrána pomocí SFTP klienta, například [FileZilla](https://filezilla-project.org/).

Přihlašovací údaje pro SFTP naleznete v nabídce "Dokumentace".

<center>
<img src="/img/lamp-sftp-info.png" class="shadow" width="500px">
</center>

<center>
<img src="/img/lamp-filezilla.png" class="shadow" width="500px">
</center>


!!! poznámka "SFTP přístup"
    SFTP přístup pro neadministrátorské uživatele může být povolen pomocí role [operátor](/apps/#operators).

## Nastavení PHP

Vlastní [nastavení PHP](http://php.net/manual/en/ini.core.php) lze přidat dvěma způsoby:

* Konfigurace Apache aplikace - `/app/data/apache/app.conf`
* Pomocí htaccess - `/app/data/public/.htaccess`

Tyto soubory lze upravit pomocí [Správce souborů](/apps#file-manager). Nastavení s [módem](http://php.net/manual/en/configuration.changes.modes.php) `PHP_INI_SYSTEM` nelze nastavit v htaccess souborech.

Příklad konfigurace htaccess:

```php
php_value post_max_size 600M
php_value upload_max_filesize 600M
php_value memory_limit 128M
php_value max_execution_time 300
php_value max_input_time 300
php_value session.gc_maxlifetime 1200
```
## Nastavení Apache

Vlastní nastavení [Apache](https://httpd.apache.org/docs/current/howto/htaccess.html) lze přidat dvěma způsoby:

* Konfigurace Apache aplikace - /app/data/apache/app.conf
* Pomocí htaccess - /app/data/public/.htaccess

Soubory výše lze upravit pomocí Správce souborů. Po provedení změn nezapomeňte aplikaci restartovat.

Příklad konfigurace htaccess:

```bash
ServerSignature Off
```

## Vlastní HTTP hlavičky

Vlastní HTTP hlavičky lze nastavit v souboru `/app/data/public/.htaccess`. Modul apache mod_headers je již povolen. Podívejte se na tento článek pro více informací.

## PHP rozšíření

Aplikace LAMP již obsahuje většinu populárních PHP rozšíření, včetně následujících:

- php-apcu
- php-cli
- php-curl
- php-fpm
- php-gd
- php-gmp
- php-imap
- php-intl
- php-json
- php-mbstring
- php-mcrypt
- php-mysql
- php-mysqlnd
- php-pgsql
- php-redis
- php-sqlite
- php-xml
- php-xmlrpc
- php-zip

Kompletní seznam předinstalovaných rozšíření naleznete v defaultním souboru index.php aplikace, který vypíše `phpInfo()`.

## Instalace vlastních PHP rozšíření

Aplikace LAMP podporuje instalaci vlastních PHP rozšíření. Jako příklad si nainstalujeme [ionCube Loader](https://www.ioncube.com/), který je často vyžadován pro instalaci komerčních PHP aplikací.

!!! poznámka "ionCube je již nainstalován" Aplikace LAMP má vestavěnou podporu pro ionCube. Níže uvedené kroky jsou pouze příkladem.

### Krok 1: Stažení rozšíření

Stáhněte a rozbalte balíčky ionCube pro Linux 64-bit (tar.gz nebo zip) z webu ionCube nebo použijte přímý odkaz.

### Krok 2: Nahrání pomocí SFTP

Nahrajte rozbalený adresář do kořenového adresáře SFTP (/app/data) aplikace OSCloud (tj. jednu úroveň nad public/).

<center>
<img src="/img/lamp-upload-ioncube.png" class="shadow" width="500px">
</center>


### Krok 3: Povolení rozšíření

V kořenovém adresáři aplikace OSCloud (v /app/data) najdete soubor php.ini.

Přidejte následující řádek pro povolení rozšíření (přidejte jej před mnoho ;extension řádků):

```bash
zend_extension=/app/data/ioncube/ioncube_loader_lin_7.2.so
```

Aplikace LAMP má deaktivovanou podporu pro thread safety, proto zvolte rozšíření bez přípony `ts`.

### Krok 4: Restart aplikace

Nakonec restartujte aplikaci, aby se povolilo rozšíření.

### Krok 5: Ověření instalace

Navštivte výchozí stránku aplikace LAMP a ověřte, zda je rozšíření povoleno.

<center>
<img src="/img/lamp-ioncube-installed.png" class="shadow" width="500px">
</center>


## Konfigurace MySQL

Přihlašovací údaje k databázi naleznete v souboru `/app/data/credentials.txt` pomocí [správce souborů](https://).

Technicky vzato jsou přihlašovací údaje MySQL zpřístupněny aplikaci jako proměnné prostředí. Tyto proměnné se mohou časem měnit. Tento přístup umožňuje OSCloud pravidelně měnit heslo k databázi jako bezpečnostní opatření a také umožňuje snadnou migraci aplikací mezi různými instalacemi OSCloud.

Zveřejněné proměnné prostředí jsou:

```bash
CLOUDRON_MYSQL_URL=            # MySQL URL (pouze pokud používáte jednu databázi)
CLOUDRON_MYSQL_USERNAME=       # Uživatelské jméno
CLOUDRON_MYSQL_PASSWORD=       # Heslo
CLOUDRON_MYSQL_HOST=           # IP adresa nebo hostname serveru
CLOUDRON_MYSQL_PORT=           # Port serveru
CLOUDRON_MYSQL_DATABASE=       # Název databáze (pouze pokud používáte jednu databázi)
```
Pokud má PHP aplikace konfigurační soubor `config.php`, který vyžaduje přihlašovací údaje k MySQL, mohou být nastaveny takto:

```php-template
'db' => array (
    'hostname' => getenv("CLOUDRON_MYSQL_HOST"),
    'username' => getenv("CLOUDRON_MYSQL_USERNAME"),
    'password' => getenv("CLOUDRON_MYSQL_PASSWORD"),
    'database' => getenv("CLOUDRON_MYSQL_DATABASE")
), // Konfigurace databáze
```

Některé aplikace zobrazují instalační obrazovku a budou vyžadovat surové přihlašovací údaje MySQL. Tyto přihlašovací údaje lze získat pomocí Správce souborů v souboru `/app/data/credentials.txt`.

<center>
<img src="/img/lamp-webterminal-mysql.png" class="shadow" width="500px">
</center>

**Důležité**  Jakmile je instalace dokončena, ujistěte se, že jste v konfiguračním souboru aplikace přešli na použití proměnných prostředí pomocí `getenv()` namísto surových přihlašovacích údajů. Jinak by budoucí aktualizace mohly aplikaci narušit.

### Přizpůsobení MySQL

Na OSCloud je server MySQL sdílen mezi všemi aplikacemi. Každá aplikace získá přihlašovací údaje bez oprávnění roota, což zajišťuje jejich vzájemnou izolaci. To znamená, že nelze nastavit MySQL specificky pro jednu aplikaci.

Nicméně mnoho [proměnných MySQL](https://dev.mysql.com/doc/refman/5.7/en/server-system-variables.html), jako například `sql_mode`, může být nastaveno na relaci úpravou vašeho kódu takto:

```php
// připojte se k MySQL a spusťte první dotaz
mysql_query("SET SESSION SQL_MODE = 'TRADITIONAL'");
mysql_query("SET SESSION UNIQUE_CHECKS = false");
mysql_query("SET SESSION FOREIGN_KEY_CHECKS=0");
```
## phpMyAdmin

phpMyAdmin je přístupný na adrese `/phpmyadmin` aplikace. Používá základní ověřování přes soubor htpasswd a je přednastaven s administrátorským účtem a vygenerovaným heslem. Heslo naleznete v souboru `phpmyadmin_login.txt`, spolu s detaily o správě dalších uživatelů.

<br/>
<center>
<img src="/img/lamp-phpmyadmin.png" class="shadow" width="500px">
</center>
<br/>


Pokud přístup přestane fungovat, jednoduše odstraňte soubor `.phpmyadminauth` a restartujte aplikaci. Tím se vygenerují nové přihlašovací údaje pro phpMyAdmin.

## Deaktivace phpMyAdmin

Je dobrým bezpečnostním postupem phpMyAdmin po jeho použití deaktivovat. Pro deaktivaci upravte soubor /app/data/apache/app.conf pomocí Správce souborů a komentujte následující řádek:

```bash
# Tento řádek můžete zakomentovat, pokud nepotřebujete přístup k PHPMyAdmin
# Include "/app/code/apache/phpmyadmin.conf"
```

Nezapomeňte aplikaci restartovat po provedení výše uvedené změny.

## Email

Na OSCloud jsou přihlašovací údaje k e-mailu zpřístupněny aplikaci jako proměnné prostředí.

Zveřejněné proměnné prostředí jsou:

```bash
CLOUDRON_MAIL_SMTP_SERVER       # SMTP server
CLOUDRON_MAIL_SMTP_PORT         # Port SMTP serveru
CLOUDRON_MAIL_SMTPS_PORT        # Port SMTPS serveru (pro legacy aplikace)
CLOUDRON_MAIL_SMTP_USERNAME     # Uživatelské jméno
CLOUDRON_MAIL_SMTP_PASSWORD     # Heslo
CLOUDRON_MAIL_FROM              # MAIL FROM adresa. Pro změnu viz [tento odkaz](/apps/#mail-from-address)
CLOUDRON_MAIL_DOMAIN            # Doména e-mailu
```

Můžete použít `getenv()` pro získání hodnot výše uvedených proměnných prostředí v kódu. Surové hodnoty lze získat pomocí Správce souborů v souboru `/app/data/credentials.txt`.

**Upozornění: Vestavěná funkce PHP mail() nefunguje** Používá lokální binární soubor sendmail, který není nakonfigurován na OSCloud.

Můžete použít [PHPMailer](https://packagist.org/packages/phpmailer/phpmailer) k odesílání e-mailů (nainstalováno pomocí composer require phpmailer/phpmailer):

```php
<?php
//Import PHPMailer classes into the global namespace
//These must be at the top of your script, not inside a function
use PHPMailer\PHPMailer\PHPMailer;
use PHPMailer\PHPMailer\SMTP;
use PHPMailer\PHPMailer\Exception;

//Load Composer's autoloader
require 'vendor/autoload.php';

//Create an instance; passing `true` enables exceptions
$mail = new PHPMailer(true);

try {
    //Server settings
    $mail->SMTPDebug = SMTP::DEBUG_SERVER;                      //Enable verbose debug output
    $mail->isSMTP();                                            //Send using SMTP
    $mail->Host       = getenv('CLOUDRON_MAIL_SMTP_SERVER');    //Set the SMTP server to send through
    $mail->SMTPAuth   = true;                                   //Enable SMTP authentication
    $mail->Username   = getenv('CLOUDRON_MAIL_SMTP_USERNAME');  //SMTP username
    $mail->Password   = getenv('CLOUDRON_MAIL_SMTP_PASSWORD');  //SMTP password
    $mail->SMTPSecure = '';
    $mail->Port       = getenv('CLOUDRON_MAIL_SMTP_PORT');

    //Recipients
    $mail->setFrom(getenv('CLOUDRON_MAIL_FROM'), 'Mailer');
    $mail->addAddress('test@cloudron.io', 'Cloudron Test');     //Add a recipient

    //Content
    $mail->isHTML(true);                                  //Set email format to HTML
    $mail->Subject = 'Here is the subject';
    $mail->Body    = 'This is the HTML message body <b>in bold!</b>';
    $mail->AltBody = 'This is the body in plain text for non-HTML mail clients';

    $mail->send();
    echo 'Message has been sent';
} catch (Exception $e) {
    echo "Message could not be sent. Mailer Error: {$mail->ErrorInfo}";
}
```
## Redis

Na OSCloud jsou přihlašovací údaje k Redis zpřístupněny aplikaci jako proměnné prostředí.

Zveřejněné proměnné prostředí jsou:

```bash
CLOUDRON_REDIS_URL          # Redis URL ve formátu redis://username:password@host:port
CLOUDRON_REDIS_HOST         # Hostname serveru Redis
CLOUDRON_REDIS_PORT         # Port serveru Redis
CLOUDRON_REDIS_PASSWORD     # Heslo Redis
```

Můžete použít `getenv()` pro získání hodnot výše uvedených proměnných prostředí v kódu. Surové hodnoty lze získat pomocí Správce souborů v souboru `/app/data/credentials.txt`.


## LDAP

Na OSCloud jsou přihlašovací údaje k LDAP zpřístupněny aplikaci jako proměnné prostředí.

Zveřejněné proměnné prostředí jsou:

```bash
CLOUDRON_LDAP_SERVER=                                # IP adresa LDAP serveru
CLOUDRON_LDAP_HOST=                                  # IP adresa LDAP serveru (stejná jako výše)
CLOUDRON_LDAP_PORT=                                  # Port LDAP serveru
CLOUDRON_LDAP_URL=                                   # URL LDAP serveru ve formátu ldap://ip:port
CLOUDRON_LDAP_USERS_BASE_DN=                         # Základní DN uživatelů LDAP ve formátu ou=users,dc=oscloud
CLOUDRON_LDAP_GROUPS_BASE_DN=                        # Základní DN skupin LDAP ve formátu ou=groups,dc=oscloud
CLOUDRON_LDAP_BIND_DN=                               # DN pro provádění požadavků LDAP
CLOUDRON_LDAP_BIND_PASSWORD=                         # Heslo pro provádění požadavků LDAP
```

Chcete-li chránit web pomocí základního ověřování LDAP, použijte následující konfiguraci Apache:

```apache
<Directory /app/data/public>
    Options +FollowSymLinks
    AllowOverride None
    Require valid-user
    AuthName "OSCloud LDAP Authentication"
    AuthBasicProvider ldap
    AuthType Basic
    AuthLDAPURL ${CLOUDRON_LDAP_URL}/${CLOUDRON_LDAP_USERS_BASE_DN}?username?sub?(username=*)
    AuthLDAPBindDN ${CLOUDRON_LDAP_BIND_DN}
    AuthLDAPBindPassword ${CLOUDRON_LDAP_BIND_PASSWORD}
</Directory>
```

## Vlastní startovací skript

Vlastní startovací skript lze umístit do `/app/data/run.sh`. Například:

```bash
#!/bin/bash

echo "Tento skript je volán před spuštěním aplikace."

# Vytvoření symlinků
rm -rf /app/data/var/cache
mkdir -p /run/cache
ln -sf /run/cache /app/data/var/cache
```

## Composer

composer, npm a další běžné nástroje jsou nainstalovány z obrazového souboru OSCloud. Pro spuštění těchto nástrojů přepněte nejprve na uživatele www-data (většina by neměla být spuštěna jako root).

```bash
su - www-data
cd /app/data/public           # zde je umístěn PHP kód
composer require drush/drush
npm install
```
!!! note "Memory limit"
Aplikace LAMP běží s 256 MB RAM jako výchozí nastavení, což nemusí být dostatečné pro Composer a další nástroje. Pokud vidíte chybovou zprávu Killed, zvyšte limit paměti aplikace na 1 GB.

## Laravel

Chcete-li spustit aplikace Laravel, viz tento článek.
Nastavení reverzní proxy

Pokud chcete například provozovat vlastní WordPress v rámci této aplikace, kód bude běžet za nginx proxy. Aplikace jako WordPress vyžadují určitý kód ve `wp-config.php`, aby tuto konfiguraci zpracovaly:

```bash
/*
 http://cmanios.wordpress.com/2014/04/12/nginx-https-reverse-proxy-to-wordpress-with-apache-http-and-different-port/
 http://wordpress.org/support/topic/compatibility-with-wordpress-behind-a-reverse-proxy
 https://wordpress.org/support/topic/wp_home-and-wp_siteurl
 */
// If WordPress is behind reverse proxy which proxies https to http
if (!empty($_SERVER['HTTP_X_FORWARDED_FOR'])) {
    $_SERVER['HTTP_HOST'] = $_SERVER['HTTP_X_FORWARDED_HOST'];

    if ($_SERVER['HTTP_X_FORWARDED_PROTO'] == 'https')
        $_SERVER['HTTPS']='on';
}
```

## Kontrola stavu

Aplikace LAMP očekává odpověď 2xx z cesty '/'. Pokud je vaše aplikace zcela chráněna, kontrola stavu může označit vaši aplikaci jako neodpovídající namísto běžící.

Můžete to obejít přidáním následujícího kódu do `/app/data/public/.htaccess`:

```apache
RewriteEngine On
RewriteCond %{HTTP_USER_AGENT} OSCloudHealth
RewriteRule ^ - [R=200]
```

Případně přidejte něco takového do config.php nebo index.php aplikace:

```php
if ($_SERVER["REMOTE_ADDR"] == '172.18.0.1') {
    echo "OSCloud kontrola stavu odpověď";
    exit;
}
```