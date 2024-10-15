# Zabezpečení

### Turnkey zabezpečení

Zabezpečení je klíčovým prvkem OSCloud. Neustále vydáváme aktualizace, které zpřísňují bezpečnostní politiky firewallu OSCloud, abychom uživatelům nabídli bezpečnost bez nutnosti manuální konfigurace.

### Ochrana soukromí a kontrola

OSCloud je navržen tak, aby poskytoval úplnou kontrolu nad daty a jejich vlastnictvím. Veškerý kód a oznámení jsou zpracovány na vašem serveru, a to bez zapojení externích služeb nebo analytik. OSCloud nekontaktuje žádné externí servery a neposkytuje třetím stranám přístup k vašim datům.

### HTTPS

Všechny aplikace běžící na OSCloud jsou přístupné pouze přes HTTPS. HTTP požadavky jsou automaticky přesměrovány na HTTPS a OSCloud spravuje SSL certifikáty pomocí Let's Encrypt, včetně jejich automatické obnovy.

### Šifrování záloh

Zálohy jsou volitelně šifrovány pomocí AES-256-CBC, což zajišťuje vysokou úroveň ochrany vašich dat při ukládání. To znamená, že i v případě, že by někdo získal přístup k zálohám, bez šifrovacího klíče nejsou data čitelná.

---

### Omezení pro hesla

- **OSCloud** vyžaduje, aby hesla uživatelů obsahovala alespoň 1 velké písmeno, 1 číslici a 1 speciální znak.
- Hesla uživatelů musí mít minimálně 8 a maximálně 256 znaků.
- Každé heslo je individuálně **saltováno** a hashováno pomocí algoritmu **PBKDF2** (viz [RFC 2898, sekce 5.1](https://www.ietf.org/rfc/rfc2898.txt)).

---

### Izolace aplikací a sandboxing

- Aplikace jsou od sebe **zcela izolované**. Jedna aplikace nemůže manipulovat s databází jiných aplikací nebo s jejich místními soubory. Toho dosahujeme pomocí **Linuxových kontejnerů**.
- Aplikace běží s **rootfs pouze pro čtení**, což zabraňuje útokům, kdy by bylo možné manipulovat s kódem aplikace.
- Aplikace se mohou připojit pouze k doplňkům, jako jsou databáze, LDAP nebo přenos e-mailů, a to **pouze pomocí ověřování**.
- Aplikace jsou spouštěny s **profilem AppArmor**, který zakazuje mnoho systémových volání a omezuje přístup k souborovým systémům **proc** a **sys**.
- Většina aplikací běží jako uživatel bez oprávnění **root**. V budoucnu plánujeme implementaci uživatelských jmenných prostorů.
- Každá aplikace je spuštěna ve své vlastní **subdoméně**, na rozdíl od dílčích cest. To zajišťuje, že zranitelnosti typu **XSS** v jedné aplikaci neohrozí ostatní aplikace.
- Procesní kapacity jako **NET_RAW** jsou vypuštěny, což zvyšuje bezpečnost.