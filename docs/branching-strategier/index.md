---
title: Branching-strategier
nav_order: 30
has_children: true
---

# Branching-strategier

Att branch:a är enkelt — `git checkout -b feature/login`. Svårare är att komma överens i teamet om **när** en branch skapas, **hur länge** den lever, och **hur** den kommer tillbaka till huvudgrenen. Det är vad en branching-strategi bestämmer.

Det finns inte ett rätt svar — olika strategier passar olika typer av produkter och releasecykler.

| Sida                    | Innehåll                                                      |
| ----------------------- | ------------------------------------------------------------- |
| Git Flow                | Den klassiska, strikta modellen med develop/release/hotfix    |
| GitHub Flow             | Enklare — main + korta feature branches + PR                  |
| Trunk-based development | Nästan inga branches alls — kontinuerlig integration mot main |
| Branch-namngivning      | Konventioner, prefix, Conventional Commits                    |
| Pull Requests           | Bra PR-beskrivningar, kodgranskning, Draft PR                 |
| Merge-strategier        | Merge vs squash vs rebase — när man väljer vad                |
