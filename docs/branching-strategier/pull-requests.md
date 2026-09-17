---
title: Pull Requests
parent: Branching-strategier
nav_order: 40
---

# Pull Requests

En Pull Request (PR) är inte bara ett tekniskt steg för att mergea kod. Det är en **konversation** — en chans att fånga buggar, dela kunskap, och se till att ingen skriver in ett helvete i `main` utan att minst en person fattat vad koden gör.

GitHub kallar det Pull Request. GitLab kallar det Merge Request. Samma sak.

## Vad är en PR, tekniskt?

Du skapar en PR när du vill mergea en branch till en annan — vanligtvis din feature branch till `main`. GitHub visar:

- Vilka commits som ingår
- En diff — exakt vilka rader som lagts till eller tagits bort
- Automatiska tester (om CI är konfigurerat) — gröna bocks eller röda kryss
- En kommentarstråd för granskning

## En bra PR börjar med en bra beskrivning

Dålig PR-beskrivning:

```
fixar kassan
```

Bra PR-beskrivning:

```markdown
## Vad gör den här PR:en?

Lägger till stöd för rabattkoder i kassan. Användaren kan nu ange
en kod vid checkout — om koden är giltig dras rabatten av på totalen.

## Hur testar man det?

1. Lägg en vara i kundvagnen
2. Gå till kassan
3. Ange koden `SOMMAR20` — ska ge 20% rabatt
4. Testa med en ogiltig kod (`FELKOD`) — ska visa felmeddelande

## Skärmdump

[bild på hur det ser ut i webbläsaren]

## Kopplade issues

Closes #42
```

`Closes #42` stänger automatiskt GitHub Issue #42 när PR:en mergas. Bra sätt att hålla ordning.

## PR-storlek — den regel de flesta ignorerar

En PR bör vara tillräckligt liten för att kunna granskas ordentligt under en kafferast. Tumregeln bland erfarna team: **under 400 ändrade rader**.

Pelle på teamet har öppnat en PR med 2 300 ändrade rader. Ingen orkar granska den ordentligt. Alla klickar "Approve" för att slippa. Buggen som borde ha fångats av granskningen hittas tre veckor senare i produktion.

Lösningen är att dela upp arbetet i mindre, logiska steg — varje steg är sin egna PR:

```
feature/kundvagn-rabattkod
├── PR 1: datamodell och API-endpoint för att validera koder
├── PR 2: UI i kassan
└── PR 3: felhantering och edge cases
```

## Kodgranskning — vad kollar man på?

En granskare läser koden med fyra frågor i bakhuvudet:

1. **Fungerar det?** — Gör koden det PR:en påstår att den gör?
2. **Är det läsbart?** — Om en ny person i teamet läser det här om sex månader — förstår de vad som händer?
3. **Bryter det något?** — Kan den här ändringen påverka något som redan fungerar?
4. **Finns det ett enklare sätt?** — Inte för att vara petig, utan för att enklare kod är mer pålitlig kod

En granskare är **inte** ansvarig för att hitta varje enskild bugg — det är testernas jobb. Granskning handlar om det mänskliga lagret.

## Konventioner för kommentarer

För att slippa missförstånd har många team börjat prefixera PR-kommentarer:

| Prefix        | Betydelse                                         |
| ------------- | ------------------------------------------------- |
| `nit:`        | Petighet, liten stil-sak — ta det eller lämna det |
| `suggestion:` | Idé, inte krav                                    |
| `question:`   | Jag förstår inte — förklara gärna                 |
| `blocker:`    | Det här måste fixas innan merge                   |

```
nit: Skulle skriva `result` istället för `res` — enklare att läsa

blocker: Om `discount` är null kraschar den här raden — behöver null-check
```

Det är trevligare att ta emot en `nit:` än att undra om granskaren menar att du måste ändra det eller inte.

## Draft PR — öppna tidigt

Vill du ha feedback redan innan koden är klar? Öppna PR:en som **Draft** (utkast):

```
GitHub → New Pull Request → Create Draft Pull Request
```

En Draft PR kör CI-testerna, syns i teamets PR-lista, och signalerar "jag jobbar på det här och vill ha tidig input — men merge:a det inte än."

Konvertera till vanlig PR när du är klar: `Ready for review`.

## Vad händer om testerna är röda?

Enkelt: du fixar det, committar, och pushar. PR:en uppdateras automatiskt. Testerna körs igen.

Mergea aldrig med röda CI-tester om inte någon annan aktivt har sagt att det är OK just nu — och även då bör du dokumentera varför i PR-beskrivningen.
