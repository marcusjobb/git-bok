---
title: De tre områdena
parent: Grunder
nav_order: 10
---

# De tre områdena

Tre begrepp förklarar hela Git-flödet:

- **Working Directory** — mappen där du faktiskt kodar. Vanlig redigering, som vanligt.
- **Staging Area** — en förberedelseplats. Du väljer vilka filer som ska ingå i nästa sparning (`git add`).
- **Repository** — den faktiska historiken. `git commit` skapar en permanent ögonblicksbild av allt som är stagat.

```mermaid
flowchart LR
    A[Working Directory<br/>du kodar här] -->|git add| B[Staging Area<br/>förbereds]
    B -->|git commit| C[Repository<br/>sparad historik, lokalt]
    C -->|git push| D[(GitHub<br/>fjärrrepository)]
    D -->|git pull| C
    style A fill:#f0f0f0,stroke:#888,color:#111
    style B fill:#f0f0f0,stroke:#888,color:#111
    style C fill:#1565c0,stroke:#0d47a1,color:#fff
    style D fill:#1565c0,stroke:#0d47a1,color:#fff
```

GitHub är ett **fjärrrepository** — en kopia av historiken som ligger online. Du synkar dit med `git push` (ladda upp) och hämtar med `git pull` (ladda ner).

## git add — Working Directory → Staging Area

Flyttar en ändring till förberedelseplatsen — du säger "ja, den här filen ska vara med i nästa sparning."

```bash
git add Program.cs    # en specifik fil
git add .             # alla ändrade filer
```

```mermaid
flowchart LR
    A[Working Directory] -->|git add| B[Staging Area]
    style A fill:#f0f0f0,stroke:#888,color:#111
    style B fill:#1565c0,stroke:#0d47a1,color:#fff
```

## git commit — Staging Area → Repository

Tar allt som är stagat och skapar en permanent ögonblicksbild i historiken.

```bash
git commit -m "Lägg till validering av e-postadress"
```

```mermaid
flowchart LR
    A[Staging Area] -->|git commit| B[Repository<br/>lokalt]
    style A fill:#f0f0f0,stroke:#888,color:#111
    style B fill:#1565c0,stroke:#0d47a1,color:#fff
```

**Vad gör ett bra commit-meddelande?** Det förklarar **vad** och **varför** — koden visar redan **hur**.

```bash
# Bra
git commit -m "Fixa krasch när lista är tom"

# Dåligt — säger ingenting
git commit -m "fix"
git commit -m "asdf"
```

Commit-historiken är din dokumentation. Tre månader senare, när du undrar varför ett beslut togs, är ett bra meddelande guld värt.

## git push / git pull — Repository ↔ GitHub

`git push` skickar din lokala historik till GitHub. `git pull` hämtar ner det som finns där men inte hos dig.

```bash
git push    # ladda upp dina commits
git pull    # hämta andras commits
```

```mermaid
flowchart LR
    A[Repository<br/>lokalt] -->|git push| B[(GitHub)]
    B -->|git pull| A
    style A fill:#f0f0f0,stroke:#888,color:#111
    style B fill:#1565c0,stroke:#0d47a1,color:#fff
```

**Varför blir push ibland avvisad?** Om GitHub har commits du inte har lokalt (t.ex. en kollega pushat före dig) säger Git nej:

```plaintext
! [rejected] main -> main (fetch first)
```

```mermaid
sequenceDiagram
    participant Du
    participant GitHub
    participant Kollega

    Kollega->>GitHub: git push (kommer in först)
    Du->>GitHub: git push
    GitHub-->>Du: ! [rejected] fetch first
    Du->>GitHub: git pull
    GitHub-->>Du: hämtar kollegans ändringar
    Du->>GitHub: git push (fungerar nu)
```

Lösningen är alltid samma: `git pull` innan `git push`. Ännu bättre vana — pulla *innan* du börjar jobba, inte bara innan du pushar.

## git clone — GitHub → din dator

Hämtar ett befintligt repo från GitHub ner till din dator — en fullständig kopia, historik och allt.

```bash
git clone git@github.com:anvandarnamn/repo-namn.git
cd repo-namn
```

```mermaid
flowchart LR
    A[(GitHub)] -->|git clone| B[Repository<br/>lokalt, med historik]
    B -.->|skapas direkt| C[Working Directory]
    style A fill:#f0f0f0,stroke:#888,color:#111
    style B fill:#1565c0,stroke:#0d47a1,color:#fff
    style C fill:#1565c0,stroke:#0d47a1,color:#fff
```

Till skillnad från `git add`/`git commit`/`git push` (som flyttar *dina* ändringar framåt steg för steg) går `git clone` motsatt väg — en engångskopia av allt, direkt från GitHub till din dator.
