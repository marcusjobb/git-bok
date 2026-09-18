---
title: Testa dig själv
description: "Testa dig själv i Grunder — Git-boken av Marcus Ackre Medina"
parent: Grunder
nav_order: 99
---

# Testa dig själv — Grunder

Utan att kolla:

1. Vilka är de tre områdena i Git, och i vilken ordning flyttar en ändring genom dem?

<details markdown="block">
<summary>Visa svar</summary>

Working Directory → Staging Area → Repository. `git add` flyttar från Working Directory till Staging Area, `git commit` flyttar från Staging Area till Repository.

</details>

2. Varför blir `git push` ibland avvisad med "fetch first"?

<details markdown="block">
<summary>Visa svar</summary>

För att GitHub har commits du inte har lokalt — t.ex. en kollega som pushat före dig. Lösningen är `git pull` innan du försöker `push` igen.

</details>

3. Vad är skillnaden mellan `git clone` och `git pull`?

<details markdown="block">
<summary>Visa svar</summary>

`git clone` hämtar ett repo för första gången — en engångskopia med hela historiken till en ny mapp. `git pull` hämtar nya ändringar till ett repo du redan har klonat.

</details>

4. Varför ska `.gitignore` skapas innan första commit, inte efteråt?

<details markdown="block">
<summary>Visa svar</summary>

Har du redan committat en känslig fil (t.ex. `secrets.json`) finns den kvar i historiken för alltid, även om du senare lägger till den i `.gitignore` och tar bort den. Du måste då rensa hela historiken, inte bara filen.

</details>
