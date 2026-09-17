---
title: Markdown-grunder
parent: Markdown & README
nav_order: 10
---

# Markdown-grunder

Markdown är ett lättviktigt märkspråk för att formatera text med vanliga tecken. En `#` gör en rubrik, `**text**` gör text fet, `` `kod` `` gör kod-formatering. GitHub renderar Markdown-filer automatiskt — en README.md visas som en snygg sida, inte som råtext.

Tänk på det som en enklare version av ordbehandlar-formatering, men i ren text som kan versionshanteras med Git.

```markdown
# Projektnamn

En kort beskrivning av vad projektet gör.

## Kom igång

1. Klona repot: `git clone ...`
2. Kör: `dotnet run`

## Teknik

- C# / .NET 10
- Körs i terminalen
```

## Vanliga konstruktioner

| Syntax | Resultat |
|--------|----------|
| `# Rubrik` | Stor rubrik (H1) |
| `## Rubrik` | Mellanstor rubrik (H2) |
| `**fetstil**` | **fetstil** |
| `*kursiv*` | *kursiv* |
| `` `kod` `` | `kod` inline |
| ` ```csharp ` | Kodblock med syntaxmarkering |
| `- punkt` | Punktlista |
| `1. punkt` | Numrerad lista |
| `[text](url)` | Länk |
| `![alt](bild.png)` | Bild |

Sida-vid-sida-tanken: råtext i Markdown ser konstig ut om du inte känner syntaxen, men renderad på GitHub blir den en ren, läsbar sida — samma fil, två vyer.
