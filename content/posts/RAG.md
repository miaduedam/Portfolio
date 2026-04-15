---
title: RAG
---

## Hvad er RAG?

RAG er en arkitektur, man kan bruge til at designe sin AI og fodre den med selvvalgt materiale.
Det sker via 3 steps:
Retrieve - her går systemet ind og finder de relevante chunks tekst fra materialet, der passer til spørgsmålet.
Augment - så lægger man de stykker tekst ind foran spørgsmålet, så ens AI kan se dem.
Generate - det er her AI'en svarer på spørgsmålet med de givne stykker tekst, frem for at gætte sig til et svar.
Det er super smart, da vi ikke behøver at blive ved med at skulle træne vores AI forfra. Vi kan bare blive ved med at fodre den med ny viden, samtidig med at man kan vinkle den som ønsket.

## Hvad har jeg brugt det til?

Jeg har valgt at lave en RAG-chatbot til min portfolio, Dobby. Jeg har fodret Dobby med mit CV, hvilket var super nemt at få på benene. Jeg har tilføjet en knowledge, hvor jeg har trukket mit CV ind og sat det på Dobby. Et tryk på publish, og så kunne jeg ellers bare begynde at spørge løs og få relevante svar tilbage.

At få den linket op til min portfolio har været en helt anden snak...
Mit første forsøg var at lave en knowledge, hvor den syncer fra website ved at bruge Jina, som jeg havde sat op med en API-nøgle. Jeg fandt frem til, at så lille som min portfolio er lige nu, skulle det ikke tage mange minutter, men efter flere forsøg på at den skulle crawle igennem siderne, måtte jeg give op.
Mit andet forsøg blev at prøve Firecrawl, hvilket jeg hurtigt fik op at køre med undersider og hele molevitten. Det var efter første forsøg en kæmpe sejr! Det gik dog hurtigt ned ad bakke, da mit gratis abonnement ikke dækker flere sider...

Jeg gik herefter tilbage og legede med Jina igen for at se om den kan hente en enkelt side, hvilket den godt kan. Jeg valgte derfor at bruge Jina, da den er simpel og hurtig til enkle sider og god til statiske sider som lige netop min portfolio.

## Hvad blev mit resultat, og hvad fik jeg ud af det?

Jeg har nu min RAG-bot Dobby, som med mine instruktioner kan svare på relevante spørgsmål vedrørende mit CV. Det kan være alt fra mine skills til hvilke teknologier jeg har erfaring med, og selvfølgelig lidt om mig. Det giver super god mening fremtidsmæssigt, hvis mulige arbejdspladser kommer ind og kigger på siden.
Fordi jeg har valgt at indsætte Dobby på min portfolio, gav det virkelig god mening at Dobby selvfølgelig også skal kunne fortælle om mine blogindlæg.
Jeg vil arbejde videre på at finde en måde at få inkluderet min GitHub-profil til Dobby, så det på et tidspunkt vil være muligt at have knowledge om mine projekter, og at Dobby kan vokse sin viden om mig endnu mere. Jeg har nu allerede fået en bedre forståelse for arkitekturen og flowet af, hvordan RAG deler dataen op i chunks, kategoriserer og sender kontekst til AI'en, som derfra kan vælge det mest relevante svar.
Alt i alt meget sjovt at arbejde med!
