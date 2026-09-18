---
title: Testa dig själv
description: "Testa dig själv i Branching-strategier — Git-boken av Marcus Ackre Medina"
parent: Branching-strategier
nav_order: 99
---

# Testa dig själv — Branching-strategier

Utan att kolla:

1. Vilken branch-typ i Git Flow mergas till **både** `main` och `develop`, och varför?

<details markdown="block">
<summary>Visa svar</summary>

`hotfix/*`. Den grenar ut från `main` för att fixa en akut produktionsbugg, och måste mergas tillbaka till `main` (så produktionen får fixen) **och** till `develop` (så buggen inte dyker upp igen i nästa release).

</details>

2. Vad är den centrala regeln i GitHub Flow som gör att man klarar sig utan `develop`- och `release`-grenar?

<details markdown="block">
<summary>Visa svar</summary>

Att `main` alltid är deploybar — varje förändring testas och godkänns (via Pull Request och CI) innan den mergas, istället för att samla upp features i en separat integrationsgren.

</details>

3. Hur kan ett team committa direkt till main flera gånger om dagen utan att visa halvfärdiga funktioner för användarna?

<details markdown="block">
<summary>Visa svar</summary>

Med feature flags — koden finns i main men är avstängd bakom ett villkor tills funktionen är klar och redo att visas, ofta för en liten testgrupp först.

</details>

4. Vilken strategi passar bäst för en produkt med schemalagda versionssläpp och flera parallellt supporterade versioner?

<details markdown="block">
<summary>Visa svar</summary>

Git Flow — de fem branch-typerna (särskilt `release/*` och möjligheten att hotfix:a en äldre version) är byggda just för det scenariot.

</details>
