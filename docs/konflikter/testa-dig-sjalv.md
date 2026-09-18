---
title: Testa dig själv
description: "Testa dig själv i Konflikter — Git-boken av Marcus Ackre Medina"
parent: Konflikter
nav_order: 99
---

# Testa dig själv — Konflikter

Utan att kolla:

1. Vad betyder `<<<<<<< HEAD`, `=======` och `>>>>>>> origin/main` i en konfliktfil?

<details markdown="block">
<summary>Visa svar</summary>

`<<<<<<< HEAD` markerar början av din version, `=======` skiljer de två versionerna åt, och `>>>>>>> origin/main` markerar slutet på serverns version. Alla tre måste tas bort manuellt när konflikten är löst.

</details>

2. Vad visar `git status` så länge en konflikt inte är löst?

<details markdown="block">
<summary>Visa svar</summary>

`both modified` för den berörda filen — det betyder att både du och någon annan har ändrat filen, och Git väntar på att du löser konflikten och kör `git add`.

</details>

3. När fungerar `git merge --abort`, och när gör den ingenting?

<details markdown="block">
<summary>Visa svar</summary>

Den fungerar om du inte redan kört `git add` och `git commit` på konflikten — då återställs allt till läget innan `git pull`. Har du redan committat händer ingenting, eftersom commiten redan är gjord.

</details>
