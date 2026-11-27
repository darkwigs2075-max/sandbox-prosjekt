# 5.3 – Test veggene

Resultater fra agenten (Copilot) i sandkassen. Punktene som krever at du kjører `sbx`-kommandoer selv er markert med **TODO**.

## a. Liste filer i C:\Users / hjemmemappen
Agenten kunne liste `/c/Users` og fant bare `ibrahim`. Inni den mappen så den bare `utvikling` (med `sandbox-prosjekt`, `kits-agent-context` og `AGENTS.md`) og en `workspace`-oppføring som ikke gikk å åpne. Agentens eget hjem (`/home/agent`) er et annet, tomt sted. Resten av PC-en var ikke synlig.

## b. Installere et program (cowsay / sympy)
Det gikk ikke. Agenten har ingen `pip`, `python3` eller `npm`. `apt-get install cowsay` feilet med «Permission denied» fordi agenten kjører som vanlig bruker (uid 1000), ikke root. Det som ikke kan installeres, kan heller ikke påvirke PC-en din.
**TODO:** Sjekk at `cowsay` ikke finnes på PC-en din etterpå.

## c. Hente en nettside som ikke er en utviklertjeneste (www.yr.no)
Blokkert. `curl https://www.yr.no` ga **HTTP 403**. Til sammenligning ga `https://github.com` **HTTP 200**.

## d. Åpne for yr.no med `sbx policy allow network www.yr.no`
**TODO:** Kjør kommandoen selv og prøv igjen. Agenten kan ikke endre sandkassens nettverksregler.

## e. Hvorfor bestemmer du og ikke agenten hvilke nettsteder som er åpne?
Hvis agenten kunne åpne nettsteder selv, ville reglene ikke beskyttet noe. En agent kan bli lurt av tekst på en nettside eller i en fil (prompt injection), og den kan gjøre feil. Reglene må ligge utenfor agentens kontroll, hos mennesket som er ansvarlig. Da kan ikke agenten sende data ut til feil sted eller laste ned skadelig innhold uten at du har sagt ja.

## f. Bytte til Open
**TODO:** Avslutt agenten og kjør `sbx policy reset` og `sbx run copilot`, og velg **Open**.

## g. Hente en nettside du ikke har åpnet for (www.vg.no)
I den nåværende modusen er den blokkert. `curl https://www.vg.no` ga **HTTP 403**.
**TODO:** Test igjen etter at du har byttet til Open.

Forskjellen på Balanced og Open (etter det jeg vet, sjekk mot kursmaterialet):
- **Balanced:** Bare kjente tjenester som utviklere trenger er åpne. Alt annet er blokkert til du åpner det.
- **Open:** Nesten alt nettverk er åpent.

**Balanced** er tryggest, siden agenten ikke kan nå ukjente nettsteder.

## Ekstra
**TODO:** Finn navnet med `sbx ls`, slett sandkassen med `sbx rm navn`, og start en ny. Sjekk om `cowsay` er borte, og om filene i `sandbox-prosjekt` fortsatt er der. Filene ligger på PC-en din, så de skal finnes fortsatt.
