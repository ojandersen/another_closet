# Teknisk dokumentation for Tema 10 eksamensprojekt – Another Closet

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
- Vi bruger **store bogstaver** til navngivning af komponenter.

## Git branches

- Vi navngiver branches efter, hvad de relaterer sig til – f.eks. footer, header, hero-section, layout, osv.

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

- Hentning af produkter fra Supabase API (via fetch i JS)
- Dynamisk visning af produkter i HTML
- Animeret banner
- Responsive burgermenu og hero med call-to-action

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
  const curl = "https://weydcspvvunwbeoolpli.supabase.co/rest/v1/AnotherCloset?select=*";

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
├── public/ # Billeder og SVG’er
│
├── src/ # Alt kildekode ligger her
│ ├── assets/  
│ ├── components/ # Genanvendelige Astro-komponenter
│ │ ├── Afsnit*.astro # Afsnit brugt på forskellige sider
│ │ ├── Hero*.astro # Hero-sektioner til forskellige sider
│ │ ├── Medlem\*.astro # Medlemssektioner med variationer
│ │ ├── Dinby.astro # Komponent til byvalg/visning
│ │ ├── Listeview.astro # Komponent til visning af produkter i liste
│ │ └── Header.astro # Fælles header/navigation
│ ├── css/
│ │ └── style.css # Global CSS-styling
│ ├── layouts/
│ │ └── Layout.astro # Layout-komponent som wrapper sider
│ └── pages/ # Alle rutesider
│ ├── index.astro # Forside
│ ├── omos.astro # "Om os"-side
│ ├── community.astro # Side om tøjfællesskaber
│ ├── fredericia.astro # By-side for Fredericia
│ ├── norrebro.astro # By-side for Nørrebro
│ ├── ribe.astro # By-side for Ribe
│ ├── roskilde.astro # By-side for Roskilde
│ ├── tilleje.astro # Info om leje af tøj
│ └── product/
│ └── [id].astro # Dynamisk produktside baseret på ID
├── package.json # Projektmetadata og afhængigheder
