---
title: Automatiseret Workflow
---

## Kontekst & Formål
I sidste uges blogindlæg legede jeg med at tilføje min første RAG til min portfolio, hvilket resulterede i at den kun havde knowledge om én enkelt side. Da jeg gennem semestret løbende vil opdatere min portfolio med nye blogindlæg og projekter, gav det mening at udvide denne knowledge og bygge et automatiseret workflow der følger med.

I dette blogindlæg fortæller jeg om hvordan jeg har opnået mit resultat, samt styrket mine færdigheder inden for prompting og tidsoptimering. Da hele dette projekt er vibe-coded med en Claude agent.

## Arkitektur
**Første trin** er at programmet finder frem til den rigtige knowledge base i Dify. Det sker ved at sende min API-nøgle til Dify, som svarer tilbage med ID'et på den knowledge base nøglen tilhører — ingen manuel konfiguration nødvendig.

**Andet trin** er at hente alle sider fra min portfolio. Det gør programmet ved at læse min sitemap.xml — en fil der automatisk genereres af GitHub Pages og indeholder en liste over alle URL'er på siden. Herfra ved programmet præcis hvilke sider der eksisterer.

**Tredje trin** er at spørge Dify hvad der allerede ligger i knowledge basen. Det returnerer en liste over eksisterende dokumenter, som programmet gemmer til sammenligning senere.

**Fjerde trin** er selve indhentningen af indhold. For hver URL i sitemappet kalder programmet Jina Reader, som scraper siden og returnerer indholdet som ren Markdown — altså kun den relevante tekst, uden navigation og HTML-rod. For at skåne Jina's servere kører det tre sider ad gangen med en lille pause mellem hvert kald.

**Femte trin** er synkroniseringen med Dify. For hver side sammenlignes URL'en med listen fra trin tre — hvis siden allerede eksisterer i knowledge basen opdateres den, hvis den er ny oprettes den. På den måde undgår vi dubletter og knowledge basen afspejler altid det aktuelle indhold på min portfolio.

## Teknologier
**Dify** er platformen jeg bruger til at hoste min RAG-chatbot. Deres Knowledge Base API gør det muligt at oprette og opdatere dokumenter programmatisk, uden at skulle gøre det manuelt via deres interface.

**GitHub-Pages** hoster min portfolio og genererer automatisk en sitemap.xml — en fil der lister alle URL'er på siden, som programmet bruger som udgangspunkt for synkroniseringen.

**Jina Reader** er en gratis web-scraper der tager en URL og returnerer sidens indhold som ren Markdown. Det er ideelt til RAG, da ren tekst giver bedre resultater i knowledge basen end rå HTML.

**Java** er sproget workflowet er skrevet i, og bruger udelukkende indbyggede biblioteker — ingen eksterne afhængigheder nødvendige.

## Diagram Af Flow
{{< img src="/images/Automatiseret-workflow.png" alt="Workflow diagram" >}}

## Hvad Har Jeg Lært
Det sværeste ved dette projekt har ikke været det tekniske, det har været at slippe kontrollen. Når man ikke selv skriver koden, er det svært at bevare overblikket, og det er let at ende i et dybt rabbithole, hvor man ikke får sat sig ordentligt ind i koden, og hurtigt kan tænke at den selvfølgelig har styr på det. Det er en balance jeg stadig skal finde.

Denne opgave har dog taget mig et step tættere på at finde den balance. Jeg blev overrasket over hvor meget en god prompt egentlig betyder — jeg har tidligere bare smidt en opgavebeskrivelse ind i en chatbot og fået et svar tilbage, uden at tænke videre over det. At sidde med en agent og se hvor stor forskel en præcis og gennemtænkt prompt gør for det endelige resultat, har været en øjenåbner!
Derudover har jeg fået en dybere forståelse for de teknologier jeg har arbejdet med, og hvordan man med relativt lidt kode kan forbinde helt forskellige systemer og få dem til at tale sammen.

## Resultat
Jeg har nu et workflow der ved manuelt start går ind og opdaterer Dify's knowledge base med det seneste indhold fra min portfolio.
Workflowet er smart nok til at skelne mellem nye og eksisterende sider, hvilket gør, at der aldrig opstår dubletter. Det betyder at Dobby altid er opdateret, så længe jeg husker at køre scriptet.

For at gøre det hurtigere arbejder programmet på 3 sider samtidigt frem for én ad gangen. For at undgå at Jina Reader opfatter det som spam, er der en bevidst pause på 600ms mellem hvert kald, hvilket generelt er god stil, så vi undgår at overbelaste den service man bruger!

Det næste naturlige skridt er at gøre det helt automatisk — så workflowet selv kører én gang om ugen og tjekker efter nyt indhold, uden at jeg behøver at gøre noget. Men det er en opgave til en anden dag!