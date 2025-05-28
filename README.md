# Teknisk dokumentation for Tema 7 gruppeprojekt – Another Closet

## Projektstruktur

Vi har bygget projektet i **Astro** med en klar struktur, der gør det nemt at navigere og samarbejde.

- **HTML-indhold** genereres i `pages/`-mappen.
- **Genanvendelige komponenter** som fx hero, navigation og footer ligger i `components/`.
- En fælles **layoutfil** (`layout.astro`) sikrer ensartet struktur på tværs af sider.
- Vi har én samlet **style.css**, der håndterer layout og styling på tværs af hele sitet.
- Alle billeder, fonte og andre assets er placeret i `public/`, så de er let tilgængelige og adskilt fra koden.

## Navngivning

- Vi bruger **små bogstaver og underscore** til navngivning af filer og mapper (f.eks. `product_list.js`).
- Tilhørende filer i HTML, CSS og JS har samme navn, fx `product_list.astro`, `product_list.css`, `product_list.js`.
- Dette gør det hurtigt at finde sammenhørende filer og bevare overblikket.

## Git branches

- Vi navngiver branches efter følgende konvention: `[navn]_[funktion]`
  - Eksempel: `Norrebro_afsnit`.
- Det sikrer, at vi kan se både funktion og ansvarlig person.

## Arbejdsflow

- Vi har **fordelt filerne**, så alle arbejdede i forskellige komponenter og sider:
  - Én har haft fokus på `index.astro` (forside og hero)
  - Én har kodet `[id].astro` og filtrering
  - Én har bygget navigation og layoutstruktur
- **Commit-beskeder** er beskrivende og simple.
- Når branches merges til main, **kommunikerer vi altid ændringer** på vores fælles chat, og reviewer hinandens ændringer inden merge og sikrer vi ikke clasher.

## Kodekonventioner

- Vi skriver funktioner som **arrow functions**, medmindre andet er nødvendigt.
- I CSS bruger vi **klasser** til styling og **id'er** til JavaScript-interaktioner.

---

# Funktionalitet

Vi har arbejdet med følgende kernefunktioner i projektet:

- ✅ Hentning af produkter fra Supabase API (via fetch i JS)
- ✅ Dynamisk visning af produkter i HTML
- ✅ Animeret banner
- ✅ Responsive burgermenu og hero med call-to-action

---

# API Endpoints

Vi bruger følgende endpoints fra Supabase til at hente data:

- `https://weydcspvvunwbeoolpli.supabase.co/rest/v1/AnotherCloset`
- `https://weydcspvvunwbeoolpli.supabase.co/rest/v1/AnotherCloset?select=*`

---

# Dokumentation af funktion

### Funktion: `getStaticPaths()`

**Beskrivelse:**  
Denne funktion henter alle produkter fra Supabase-databasen og genererer en liste af paths (ruter) til hver produktside. Funktionen bruges af Astro til at bygge statiske sider dynamisk for hvert produkt, så de kan tilgås via individuelle URLs.

**Parametre:**
Ingen – funktionen kaldes automatisk af Astro under build-processen.

**Returnerer:**  
En array af objekter med params og props, som Astro bruger til at generere statiske ruter. Hver params.id svarer til produktets ID i databasen.

**Eksempel:**

```javascript
export async function getStaticPaths() {
  const curl =
    "https://weydcspvvunwbeoolpli.supabase.co/rest/v1/AnotherCloset?select=*";

  const apikey = "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...";
  const options = {
    headers: {
      apikey: apikey,
    },
  };

  const response = await fetch(curl, options);
  const data = await response.json();

  return data.map((post) => {
    return {
      params: { id: post.id.toString() },
      props: { post },
    };
  });
}
```

# STRUKTUR

/
├── public/
│
├── src/
│ ├── assets/
│ ├── components/
│ │ ├── Afsnit.astro
│ │ ├── Afsnitforside.astro
│ │ ├── Afsnitforside2.astro
│ │ ├── Afsnitforside3.astro
│ │ ├── Banner.astro
│ │ ├── Dinby.astro
│ │ ├── Footer.astro
│ │ ├── Fredericia_afsnit.astro
│ │ ├── Header.astro
│ │ ├── Hero.astro
│ │ ├── Hero2.astro
│ │ ├── Hero3.astro
│ │ ├── Listeview.astro
│ │ ├── Medlem.astro
│ │ ├── Medlem2.astro
│ │ ├── Medlem3.astro
│ │ ├── Medlem4.astro
│ │ ├── Nørrebro_afsnit.astro
│ │ ├── Ribe_afsnit.astro
│ │ ├── Roskilde_afsnit.astro
│ │ ├── Tekststykke_1.astro
│ │ ├── Tekststykke_2.astro
│ │ └── Tisvilde.astro
│ ├── css/
│ │ └── style.css
│ ├── layouts/
│ │ └── Layout.astro
│ └── pages/
│ ├── index.astro
│ ├── omos.astro
│ ├── community.astro
│ ├── fredericia.astro
│ ├── norrebro.astro
│ ├── ribe.astro
│ ├── roskilde.astro
│ ├── tilleje.astro
│ └── product/
│ └── [id].astro
├── package.json
