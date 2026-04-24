---
title: AI-Agenter 
---

Jeg vil i dette blog-post gennemgå, hvordan jeg har brugt en agent til at bygge et website ud fra kundekrav, samt sætte et par ord på hvad jeg har fået af faglig forståelse for ai-agenter.

### Hvad Er En Agent
En agent er et ai-system, der opererer i en loop, hvor den har adgang til eksterne værktøjer, den kan kalde, og den bruger resultatet til at beslutte hvad den gør næste gang, da den fortsætter indtil det definerede mål er nået.

### Hvordan Virker Agenter
En agent består af 4 centrale dele.

**LLM** - er agentens hjerne.

**Tools** - giver den handlingsevne.

**Context window** - er agentens hukommelse.

**Memory og state** - agenten har ingen hukommelse på tværs af sessioner.

**Agentic loop** - også kaldet ReAct-mønsteret (Reasoning + Acting). Alle agenter følger det samme grundlæggende loop.

{{< img src="images/Agentic-loop.png" alt="Agentic-loop" >}}

### Agent VS Chatbot
Det der adskiller en agent fra et chat-system er tre ting.

**Handlingsevne** - den påvirker sin omverden.

**Målorienterethed** - er målet nået? Nej - ny strategi.

**Multi-step reasoning** - løser komplekse opgaver ved at nedbryde dem i sekvenser af mindre handlinger.

Den nemmeste måde at se forskellen på er ved at skrive til en chatbot og en agent. Den ene vil give dig et svar, hvorimod den anden vil give dig en færdig eksekveret løsning.

### Nu Til Mit Projekt!
Min lærer har taget kunde-brillerne på og fremlagt et website, han har bygget. Det er en meditations-side, hvor man kan køre igennem et minikursus i form af at høre lydklip af meditation. Han ønsker i alt 5 quiz, en under hver lektion, for at se om lytterne også har hørt hvad der faktisk er blevet sagt.

**Krav til siden:**

* Man skal ikke være logget ind.
* Det skal være muligt at huske tidligere svar fra quiz.
* Bruger skal kunne se tidligere svar, samt prøve igen.

Første step var her at få lavet en god prompt til min agent! Jeg kunne allerede denne gang mærke, jeg var meget stærkere og teknisk i min prompting. Jeg brugte igen samme metode som sidst med at skrive prompten sammen med min chatbot. 

Jeg blev denne gang også introduceret til plan-mode, som er en planlægningstilstand, hvor agenten ikke kører i det normale agentic loop, men planlægger uden at handle. Det fungerede super godt, da jeg satte min prompt ind og fik lukket de sidste huller og sørget for, at agenten og jeg er på samme bølgelængde, inden den går helt banjo!

For at starte simpelt valgte jeg at tilføje én quiz for at få et velfungerende site. Et problem vi så i mange demoer, var at quizzen blev gjort til én lang med de 29 spørgsmål. Det undgik jeg heldigvis ved at starte med den ene og sørge for via min prompt, at det ville være nemt at tilføje flere.

{{< img src="images/Prompt-1.png" alt="Prompt" >}}

Jeg tog her også et valg, sammen med anbefaling fra chatbot, om at gemme quizzerne i localStorage for at opnå kundens krav om, at det skulle være muligt for brugeren at se tidligere svar.

{{< img src="images/Prompt-2.png" alt="Prompt" >}}

Derefter er der faktisk ikke meget mere at sige, end at det gik forfærdeligt smooth. Den ramte plet på det billede, jeg havde af designet, og sitet i sig selv. Jeg sidder igen tilbage og tænker waow, men faktisk også puha, hvordan kommer det til at se ud for mig på arbejdsmarkedet om et par år. Når et projekt, der ville tage mig flere uger i et team, tager den 10 minutter. Men i sidste ende tror jeg ikke, det handler om at blive erstattet, men at det handler om at lære at styre den rigtigt. Hvilket er præcis det, jeg er i gang med!