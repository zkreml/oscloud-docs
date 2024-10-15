# Certifikáty

Na OSCloud se staráme o bezpečnost a spolehlivost vaší komunikace tím, že všechny aplikace a webové stránky jsou chráněny pomocí SSL/TLS certifikátů. Tyto certifikáty zajišťují šifrovaný přenos dat mezi vaším prohlížečem a serverem, čímž zabraňují neoprávněnému přístupu a odposlechu.

## Automatická správa certifikátů

OSCloud využívá službu Let's Encrypt, která poskytuje zdarma SSL/TLS certifikáty. Všechny certifikáty jsou automaticky:

- Vygenerovány při prvním nasazení aplikace.
- Pravidelně obnovovány (Let's Encrypt certifikáty mají 90denní platnost).
- Automaticky nainstalovány na příslušné aplikace.

## Wildcard certifikáty

OSCloud podporuje také Wildcard certifikáty od Let's Encrypt, což znamená, že jeden certifikát může chránit všechny subdomény vaší domény (např. \*.example.com). Wildcard certifikáty poskytují další vrstvu bezpečnosti tím, že zamezují odhalení jednotlivých subdomén veřejně dostupnými nástroji pro kontrolu certifikátů.

## HTTPS všude

Všechny aplikace na OSCloud jsou dostupné výhradně přes protokol HTTPS. Pokud někdo zadá URL pomocí HTTP, server automaticky přesměruje požadavek na HTTPS. Tím zajišťujeme, že veškerá komunikace je vždy šifrovaná a bezpečná.

## HSTS (Strict-Transport-Security)

OSCloud využívá hlavičku Strict-Transport-Security (HSTS), která zajišťuje, že webové prohlížeče komunikují se serverem vždy přes HTTPS a zabrání potenciálním útokům typu downgrade attack (útok na snížení úrovně šifrování).

## Transparentnost certifikátů

Let's Encrypt automaticky zapisuje všechny vydané certifikáty do Certificate Transparency Logs, což je mechanismus pro zajištění důvěryhodnosti a kontrolovatelnosti certifikátů. U Wildcard certifikátů je výhodou, že neodhalují jednotlivé subdomény, což zvyšuje bezpečnost a soukromí.
