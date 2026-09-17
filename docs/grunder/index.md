---
title: Grunder
nav_order: 10
has_children: true
---

# Grunder

Git är ett versionshanteringssystem — en tidsmaskin för din kod. Det håller koll på varje ändring du gör, så du alltid kan gå tillbaka och se hur ett projekt såg ut igår, förra veckan, eller dagen innan allt gick sönder.

Utan Git slutar det ofta såhär:

```plaintext
projekt/
├── Program.cs
├── Program_gammal.cs
├── Program_fungerar.cs
├── Program_final.cs
└── Program_final_RIKTIG.cs
```

Med Git finns det alltid bara **en** version av varje fil. Historiken sparas i bakgrunden — du behöver aldrig döpa en fil till "RIKTIG" igen.

| Sida | Innehåll |
|------|---------|
| De tre områdena | Working Directory, Staging Area, Repository |
| Vanliga kommandon | status, add, commit, push/pull, clone, init |
| SSH-nyckel & .gitignore | Ansluta säkert, hålla skräp borta från historiken |
