---
title: git tag
parent: Kommandon
nav_order: 155
---

# git tag

Sätt ett namn på en specifik commit — vanligtvis för att markera en release.

```bash
git tag v1.2.0
```

Skapar en "lightweight tag" på nuvarande HEAD.

## Annoterade tags (föredra dessa)

```bash
git tag -a v1.2.0 -m "Version 1.2.0 — stöd för rabattkoder"
```

En annoterad tag innehåller metadata: vem som skapade den, när, och ett meddelande. Det som visas på GitHub Releases.

## Tagga en specifik commit

```bash
git tag -a v1.1.0 -m "Version 1.1.0" 9d2e1f0
```

Bra om du glömde tagga vid releasetillfället.

## Lista tags

```bash
git tag
git tag -l "v1.*"    # filtrera med mönster
```

## Push tags

Tags pushas inte automatiskt med `git push`. Du måste göra det explicit:

```bash
git push origin v1.2.0    # en specifik tag
git push --tags            # alla lokala tags
```

## Ta bort en tag

```bash
git tag -d v1.2.0                         # lokalt
git push origin --delete v1.2.0           # på remote
```

## Semantic versioning — konventionen

De flesta projekt följer `MAJOR.MINOR.PATCH`:

| Del | Ökar när |
|-----|----------|
| `MAJOR` | Du gör ändringar som inte är bakåtkompatibla |
| `MINOR` | Du lägger till ny funktionalitet, bakåtkompatibelt |
| `PATCH` | Du fixar buggar, bakåtkompatibelt |

`v1.2.0` → `v1.2.1` (buggfix) → `v1.3.0` (ny feature) → `v2.0.0` (breaking change)
