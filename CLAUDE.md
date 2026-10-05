# CLAUDE.md

## Table sizing standard (new tables only)

Applies only to tables created from now on in `manual.html` / `MANUAL-COMANDOS.md`. Existing tables keep their current widths; do not change them.

When creating a new "Comando | O que faz" table (or any table whose first column holds code):

1. Size the first column so the code wraps onto at most 2 lines, with comfortable spacing and padding like the existing tables. Do not make the column hug the longest command.
2. Balance both columns per row: avoid one side with 3 lines and the other with 1. Prefer 2 lines on both sides.
3. The first column is at most 65% of the table. Only if a command still does not fit in 2 lines at 65%, allow a third line.
4. Tables whose first column is very short (symbols, single words) keep that column narrow, and the second column takes the rest.
5. New tables get no name and follow the default automatically.
6. If a new table does not look right with the default, tell me. After I approve a manual adjustment, give that table its own id and a rule scoped to it. Every exception has a name.
7. Never use :first-of-type or :nth-of-type to target a table.
8. Never rename or change a named table unless I ask.
9. The copy button stays next to the command, never alone on a separate line.
10. After creating a table, check it visually (including a narrow screen) before asking for approval.

## Named exceptions

- `tabela-exemplos` (2.5 Símbolos, Exemplos): columns 56/44 on wide screens, and 40/60 at 860px or less (the same breakpoint where the sidebar leaves the side). On wide screens, the long URL command (`! git remote set-url origin https://github.com/SaBurle/NomeDoRepo.git`) needs 2 lines with the copy button beside it.
