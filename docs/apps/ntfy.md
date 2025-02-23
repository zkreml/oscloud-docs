# <img src="/img/ntfy-logo.png" width="25px"> Ntfy 

## Ntfy

Ntfy je jednoduchá oznamovací služba **pub-sub** založená na HTTP, která implementuje specifikaci poskytovatele **UnifiedPush**. Umožňuje vám posílat upozornění na váš telefon nebo plochu pomocí skriptů z jakéhokoli počítače, zcela bez registrace, nákladů nebo složitého nastavení. Je to také **open source**, pokud chcete provozovat vlastní instanci.

Push notifikace doručované do mobilních aplikací **Matrix** jsou obvykle pouze probuzeními aplikace a nenesou skutečné užitečné zatížení (např. textové zprávy). I ve výchozím nastavení (bez použití Ntfy) zůstává obsah vašich zpráv **soukromý**, přestože prochází servery Google (Android) nebo Apple (iOS).

**Ntfy** je užitečné pro **zlepšení soukromí** a **nezávislosti** Matrixu, protože ani tato „aplikační probuzení“ již nemusí procházet servery Google/Apple. Místo toho jsou doručována přes **vlastní instanci Ntfy**.

## Použití Ntfy s UnifiedPush
Chcete-li používat **ntfy**, potřebujete mobilní aplikaci, která podporuje **UnifiedPush** jako alternativní backend pro oznámení push.

### Android

1. **Nainstalujte aplikaci distributora UnifiedPush.**
   - Příklad: **Ntfy** ([Zdrojový kód](https://github.com/binwiederhier/ntfy), [F-Droid](https://f-droid.org/packages/io.heckel.ntfy/), [Google Play](https://play.google.com/store/apps/details?id=io.heckel.ntfy))

2. **Otevřete nastavení aplikace** a nastavte svého poskytovatele **UnifiedPush** (server Ntfy) jako výchozí server.
   - Server: `https://ntfy.arch-linux.cz`

3. **Otevřete jakoukoli kompatibilní Matrix klientskou aplikaci** (např. **SchildiChat, Element**) a v **nastavení oznámení** přepněte poskytovatele oznámení na **ntfy**.

## Další využití Ntfy
Ntfy lze použít nejen s Matrixem, ale také s dalšími aplikacemi a službami:

- **Uptime Kuma** – Pro monitorování služeb lze přidat Ntfy jako endpoint pro upozornění.
- **Mastodon klienty (např. Tusky)** – Lze využít UnifiedPush k doručování notifikací.
- **Automatizované skripty** – Notifikace o dokončených úlohách nebo změnách stavu systémů.

**Ukázka nastavení:**

![Nastavení aplikace Ntfy](IMG_20230106_104630.jpg)
![Nastavení oznámení aplikace Element](IMG_20230106_104630.jpg)
