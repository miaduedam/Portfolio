---
title: AI-Applikation
---

## Intro & Formål
Jeg har denne gang arbejdet med at udvikle en ai-drevet applikation, hvor jeg bruger en sprogmodel som ekstern service via et API. 
	
Mere i dybden har jeg udviklet et system som kan give en første vurdering af en studenteropgave ved hjælp af en rubrik, som bliver vurderet af følgende materiale jeg har fået tildelt:
- studenteropgaver
- Læringsmål
- Krav til rapport 
- Dare, share, care
	
Jeg vil igennem dette blog-post tage jer med igennem processen samt sætte et par ord på hvad der bare fungerede og hvad der fungerede mindre godt.

## Flow
Jeg valgte at opdele arbejdet i to adskilte faser: først at få rubrikken og promptdesignet på plads, og dernæst at bygge selve applikationen. 

**1 fase** startede jeg med at arbejde udelukkende i Claude chatbot. Her fortalte jeg hvilke materialer vurderingen skulle baseres på, vi arbejdede os frem mod en rubrik med fem kriterier og tre niveauer hver. Det tog tre iterationer, før jeg var tilfreds med både system-prompten og user-prompten. Det vigtige var at holde dette arbejde adskilt fra selve kodningen, så jeg ikke blandede to komplekse problemer sammen på én gang.

**2 fase** var rubrikken klar, så jeg gik tilbage til Claude chatbot med en ny opgave: at generere en meget præcis og detaljeret prompt til at bygge hele monorepo-strukturen fra bunden. Jeg beskrev tech stack, mappestruktur, API-kontrakt, system-prompt, user-prompt og CI/CD-setup i én samlet specifikation, og fik her et komplet startpunkt ud af det:

```text
praktik-evaluator/
├── 📁 backend/
│   ├── 📁 src/main/java/dk/ek/
│   │   ├── Main.java
│   │   ├── 📁 controller/
│   │   │   └── EvaluationController.java
│   │   ├── 📁 service/
│   │   │   └── OpenAiService.java
│   │   └── 📁 model/
│   │       └── EvaluationRequest.java
│   └── pom.xml
│
├── 📁 frontend/
│   ├── 📁 src/
│   │   ├── App.jsx
│   │   └── main.jsx
│   └── package.json
│
└── 📁 .github/
    └── 📁 workflows/
        └── ci.yml
```
**3 fase** blev med strukturen på plads, implementationen af backend og frontend.

*Backend:* skrevet i Java med Javalin. Rubrikken og system-prompten blev hardcodet som konstanter i OpenAiService, og user-prompten bygges dynamisk ved hvert kald. API-nøglen hentes udelukkende fra miljøvariablen ANTHROPIC_API_KEY – aldrig hardkodet.

*Frontend:* bygget i React med Vite og plain CSS. Brugeren uploader en .txt eller .md fil via drag-and-drop, og resultatet vises struktureret med farvekodede niveauer, styrker, forbedringsområder og eksamensspørgsmål. Jeg tilføjede også en historikfunktion som gemmer i localstorage og en rubrikvisning direkte i appen.

**4 fase** satte jeg et GitHub Actions-workflow op, der kører på hvert push til main. Backenden kompilerer med Maven og Java, frontend-jobbet kører npm install og npm run build.

## Hvad Var Udfordrende 
Jeg synes grundlæggende ikke at projektet som helhed var specielt udfordrende, Men det var selvfølgelig ikke helt smertefrit!

Jeg mærkede først og fremmest problemer, da jeg ikke havde arbejdet med et monorepo før, selvom mappestrukturen var enkel nok, syntes jeg det var svært at finde rundt, samt vide hvilke mapper man skulle stå i for at køre kommandoer.

Jeg oplevede også udfordringer da den prompt jeg fik genereret til monorepo-strukturen oprindeligt var skrevet til OpenAI's API. Jeg valgte at bruge Anthropic i stedet, men vidste faktisk ikke at de to API'er fungerer på forskellige måder. Både i forhold til hvordan beskeder struktureres, samt hvilke endpoint og headers der bruges. Det gav en del forvirring og indsigt, da jeg pludselig ikke helt forstod hvorfor og hvilke fejl der opstod!

## Opsamling & Læring
Når jeg kigger tilbage på projektet, er det tydeligt at udfordringerne ikke kom fra selve AI-integrationen, men kom fra alt det omkring. At navigere i en ny projektstruktur, og at arve en konfiguration der ikke passede til det API jeg faktisk brugte, var begge situationer hvor jeg ikke bare kunne copypaste mig videre. Jeg var nødt til at forstå hvad der skete.

Hvilket egentlig er den vigtigste ting jeg tager med mig! 
AI kan generere et imponerende startpunkt på meget kort tid, men det erstatter ikke forståelsen. Fejlene jeg løb ind i opstod præcis der, hvor jeg faktisk troede at koden bare virkede, uden at have sat mig ind i hvad den rent faktisk gjorde. Det er en god påmindelse om at have hovedet med, også når værktøjerne er kraftfulde.

Til gengæld har projektet givet mig en meget mere konkret forståelse af prompt engineering. Det at jeg isolerede rubrik- og promptarbejdet som sin egen fase, inden jeg rørte koden, var en beslutning der betalte sig.
- System-prompten sætter kontrakten
- User-prompten leverer data

Da jeg fik de to prompts i den rigtige retning var outputtet overraskende stabilt og konsekvent, hvilket var ret fedt at opleve i praksis.

Monorepo-strukturen tager jeg også med videre. Når frontend og backend er så tæt forbundne, er det en naturlig og overskuelig måde at organisere et projekt på, når man først har fundet rundt i det selvfølgelig! 

Alt i alt, har det været super lærerigt, med nye teknikker og udfordringer!
