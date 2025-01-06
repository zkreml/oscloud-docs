# <img src="/img/findmydevice-logo.png" width="25px"> FindMyDevice App

**FindMyDeviceServer** je open-source platforma pro sledování a ovládání zařízení (například telefonu) s důrazem na bezpečnost, soukromí a transparentnost. Naše instance je dostupná na [findmydevice.oscloud.cz](https://findmydevice.oscloud.cz) a je připravena k použití.

<center>
<img src="/img/findmydevice.png" class="shadow" width="500px">
</center> 
---

## Výhody a vlastnosti

1. **Open-source**  
   Zdrojový kód je dostupný [na GitLabu](https://gitlab.com/Nulide/findmydeviceserver), což umožňuje komunitní audit a zajištění maximální transparentnosti.

2. **End-to-End šifrování**  
   Veškerá citlivá data jsou šifrována na straně zařízení uživatele a dešifrována pouze lokálně v prohlížeči.

3. **Ochrana soukromí**  
   Vaše data nejsou sdílena ani prodávána třetím stranám. Server uchovává pouze minimální množství nezbytných dat.

4. **Snadné použití**  
   Použijte naši instanci [findmydevice.oscloud.cz](https://findmydevice.oscloud.cz) bez nutnosti vlastní instalace serveru.

5. **Dostupnost aplikace**  
   Mobilní aplikaci pro Android najdete na [F-Droidu](https://f-droid.org/packages/de.nulide.findmydevice/).

---

## Jak začít?

### 1. Nastavte aplikaci Ntfy

**Co je Ntfy?**  
Ntfy je open-source aplikace pro push notifikace. FindMyDevice používá Ntfy k zasílání upozornění na vaše zařízení.

**Jak nastavit Ntfy?**

1. **Nainstalujte F-Droid**  
   Pokud ještě nemáte, nainstalujte si aplikaci F-Droid:  
   - Otevřete [f-droid.org](https://f-droid.org) a stáhněte instalační balíček (.apk).  
   - Povolte instalaci z neznámých zdrojů a dokončete instalaci.  

2. **Nainstalujte aplikaci Ntfy**  
   - Otevřete F-Droid.  
   - Vyhledejte **Ntfy** nebo použijte [přímý odkaz](https://f-droid.org/packages/io.heckel.ntfy/).  
   - Klikněte na **Install** a potvrďte instalaci.  

3. **Nastavte Ntfy**  
   - Otevřete aplikaci Ntfy a přejděte do nastavení (ikona vpravo nahoře).  
   - Do položky **„Výchozí server“** zadejte český server:  
     ```plaintext
     https://ntfy.arch-linux.cz
     ```
   - V sekci **„Protokol připojení“** vyberte **WebSockets**.  

4. **Optimalizace baterie**  
   - V nastavení systému vypněte u aplikace Ntfy různé optimalizace baterie, aby byla schopna přijímat notifikace v reálném čase.  

---
<center>
<img src="/img/ntfy1.png" class="shadow" width="500px">
</center> 
<center>
<img src="/img/ntfy2.png" class="shadow" width="500px">
</center> 


### 2. Instalace F-Droidu

**Co je F-Droid?**  
F-Droid je alternativní obchod s aplikacemi pro Android, který nabízí open-source aplikace bez reklam a sledování.

**Jak nainstalovat F-Droid?**  
1. Otevřete prohlížeč na svém zařízení a navštivte oficiální stránku [f-droid.org](https://f-droid.org).  
2. Stáhněte instalační balíček (.apk) kliknutím na tlačítko **Download F-Droid**.  
3. Povolte instalaci z neznámých zdrojů:  
   - Otevřete **Nastavení** > **Zabezpečení**.  
   - Povolte instalaci aplikací z prohlížeče, který jste použili ke stažení.  
4. Nainstalujte aplikaci F-Droid kliknutím na stažený soubor .apk.  

---

### 3. Instalace aplikace FindMyDevice

1. Otevřete aplikaci F-Droid.  
2. Vyhledejte **FindMyDevice** nebo použijte [přímý odkaz](https://f-droid.org/packages/de.nulide.findmydevice/).  
3. Klikněte na **Install** a potvrďte instalaci.

---
<iframe title="Nastavení Ntfy a FindMyDevice" width="560" height="315" src="https://peertube.arch-linux.cz/videos/embed/6e61fb71-a275-4198-9cb7-71829ad758cf" frameborder="0" allowfullscreen="" sandbox="allow-same-origin allow-scripts allow-popups allow-forms"></iframe>

### 4. Registrace zařízení

1. Otevřete aplikaci **FindMyDevice** na svém telefonu.  
2. Zadejte své **FMD ID** (unikátní identifikátor) a vytvořte si **heslo**.  
3. Vaše zařízení bude zaregistrováno na instanci [findmydevice.oscloud.cz](https://findmydevice.oscloud.cz).


---

### 5. Použití webového rozhraní

1. Přihlaste se na [findmydevice.oscloud.cz](https://findmydevice.oscloud.cz) pomocí svého FMD ID a hesla.  
2. Můžete:
   - Odesílat příkazy do zařízení.
   - Sledovat polohu zařízení.
   - Přistupovat k dalším datům, jako jsou obrázky nebo stav baterie.

---

## Podpora a zdroje

- Oficiální repozitář: [FindMyDeviceServer na GitLabu](https://gitlab.com/Nulide/findmydeviceserver)  

---

## Závěr

FindMyDeviceServer na [findmydevice.oscloud.cz](https://findmydevice.oscloud.cz) je moderní a bezpečný nástroj pro lokalizaci a ovládání vašich zařízení. Díky integraci s aplikací Ntfy a end-to-end šifrování poskytuje plnou kontrolu nad vašimi daty. Vyzkoušejte ho ještě dnes!
