# 🅰️ Angular - Guide Complet de Veille Technologique 2026

Bienvenue dans mon document de suivi pour Angular. Ce README est conçu pour centraliser toutes les connaissances essentielles, des fondamentaux aux fonctionnalités les plus avancées, en passant par les nouveautés des dernières versions et les ressources pour rester à jour.

---

## 📋 Table des Matières

1. [Fondamentaux Core](#-1-fondamentaux-core)
2. [Nouvelles Fonctionnalités par Version](#-2-nouvelles-fonctionnalités-par-version)
3. [Fonctionnalités Avancées & Design Patterns](#-3-fonctionnalités-avancées--design-patterns)
4. [Bibliothèques & Écosystème](#-4-bibliothèques--écosystème)
5. [Ce qui Change / Ce qui Disparaît](#-5-ce-qui-change--ce-qui-disparaît)
6. [Roadmap 2026-2027](#-6-roadmap-2026-2027)
7. [Ressources pour la Veille](#-7-ressources-pour-la-veille)

---

## 🧱 1. Fondamentaux Core

### Architecture Moderne

- [ ] **Standalone Components (par défaut)** : Plus besoin de `NgModule` pour les nouveaux composants. L'application entière peut être standalone.
- [ ] **Fonction `bootstrapApplication()`** : Démarrer une application sans `AppModule`.
- [ ] **`provide()` functions** : Configuration des fonctionnalités (routage, HTTP, etc.) via des fonctions provider.

### Nouvelle Syntaxe de Template (Control Flow)

- [ ] **`@if (condition) { ... } @else { ... }`** : Remplaçant de `*ngIf`.
- [ ] **`@for (item of items; track item.id) { ... } @empty { ... }`** : Remplaçant de `*ngFor`.
- [ ] **`@switch (value) { @case 'x': ... @default: ... }`** : Remplaçant de `*ngSwitch`.

### Reactivité avec Signals

- [ ] **`signal()`** : Créer un état mutable.
- [ ] **`computed()`** : Dériver des valeurs automatiquement mises à jour.
- [ ] **`effect()`** : Exécuter des effets secondaires lors des changements.
- [ ] **`input()` / `output()`** : Nouvelle façon de définir les entrées/sorties des composants.
- [ ] **`model()`** : Liaison bidirectionnelle avec deux-way binding.
- [ ] **`viewChild()` / `contentChild()`** : Requêtes basées sur les signals.

### Injection de Dépendances

- [ ] **Fonction `inject()`** : Privilégier cette approche plutôt que l'injection par constructeur.
- [ ] **`EnvironmentInjector`** : Comprendre les contextes d'injection (runInContext, etc.).
- [ ] **`@Injectable({ providedIn: 'root' })`** : Services singleton.

### Zoneless Change Detection

- [ ] **Comprendre le fonctionnement sans Zone.js** : La détection de changement est déclenchée uniquement par les Signals.
- [ ] **Configuration `provideZonelessChangeDetection()`** : Activer le mode zoneless.

### Routage

- [ ] **`provideRouter()`** : Configuration du routeur avec les nouvelles APIs.
- [ ] **`withComponentInputBinding()`** : Lier automatiquement les paramètres de route aux `@Input()`.
- [ ] **`withViewTransitions()`** : API de transition de vue native.

---

## 🚀 2. Nouvelles Fonctionnalités par Version

### ✅ Angular 17 (Novembre 2023)

- [x] **Nouveau control flow (developer preview)** : Introduction de `@if`, `@for`, `@switch`.
- [x] **Amélioration des performances de build** : esbuild par défaut pour `ng serve`.
- [x] **Support de TypeScript 5.2**.
- [x] **`@defer` (developer preview)** : Chargement différé de blocs de template.

### ✅ Angular 18 (Mai 2024)

- [x] **Zoneless (developer preview)** : Première implémentation.
- [x] **Amélioration des route guards** : API plus flexible.
- [x] **`@let` syntax (experimental)** : Déclaration de variables locales dans les templates.
- [x] **Material 3** : Support complet du design Material 3.

### ✅ Angular 19 (Novembre 2024)

- [x] **`linkedSignal()`** : Nouveau signal lié à l'état d'un autre signal.
- [x] **`outputFromObservable()` / `outputToObservable()`** : Interopérabilité améliorée avec RxJS.
- [x] **Hot Module Replacement (HMR) amélioré** : Rechargement plus rapide.
- [x] **`@defer` stable** : Officiellement prêt pour la production.

### ✅ Angular 20 (Mai 2025)

- [x] **Control flow stable et par défaut** : L'ancienne syntaxe dépréciée.
- [x] **Signal Forms (developer preview)** : Premiers formulaires basés sur les signals.
- [x] **Angular DevTools améliorées** : Debuggage avancé des signals.
- [x] **Support d'ESBuild pour les tests unitaires**.

### ✅ Angular 21 (Novembre 2025)

- [x] **Signal Forms (stables)** : `FormGroup`, `FormControl`, etc. basés sur les signals.
- [x] **Zoneless (stable)** : Prêt pour la production sans Zone.js.
- [x] **Vitest par défaut** : Nouveau test runner plus rapide.
- [x] **Amélioration des performances de compilation** : Jusqu'à 50% plus rapide.

### 🔄 Angular 22 (Mai 2026 - Actuel)

- [ ] **`ChangeDetectionStrategy.OnPush` par défaut** pour tous les nouveaux composants.
- [ ] **Suppression de l'ancien control flow** (`*ngIf`, `*ngFor` ne fonctionnent plus).
- [ ] **Angular Aria (developer preview)** : Composants "headless" accessibles.
- [ ] **Sélecteurs optionnels (experimental)** : Importer des composants sans nom de sélecteur.
- [ ] **Optimisation du bundle** : Réduction de 15% de la taille par défaut.

### 🔮 Angular 23 (Novembre 2026 - Prévisionnel)

- [ ] **Sélecteurs optionnels (stable)**.
- [ ] **Support natif des Web Components** amélioré.
- [ ] **Hydratation partielle** : SSR avec hydratation progressive.

---

## 🏗️ 3. Fonctionnalités Avancées & Design Patterns

### State Management

- [ ] **Signal Store (NgRx/Elf)** : Stores basés sur les signals pour une gestion d'état locale et globale.
- [ ] **Intégration RxJS ↔ Signals** :
  - [ ] `toSignal()` : Convertir un Observable en Signal.
  - [ ] `toObservable()` : Convertir un Signal en Observable.
- [ ] **État global avec services et signals** : Pattern simple sans bibliothèque externe.

### Performance

- [ ] **`@defer` avec triggers** : Charger des parties de l'UI en fonction d'interactions, du viewport, etc.
  - [ ] `on viewport`
  - [ ] `on interaction`
  - [ ] `on hover`
  - [ ] `on timer`
- [ ] **Virtual Scrolling** : Avec `@angular/cdk/scrolling`.
- [ ] **Lazy loading de composants** : Charger des composants indépendamment des routes.
- [ ] **Image Optimization** : Directive `NgOptimizedImage`.

### Tests

- [ ] **Vitest** : Nouveau framework de test unitaire.
- [ ] **Testing Harnesses** : Pour les tests de composants Material/CDK.
- [ ] **Test des signals** : Vérifier les valeurs de signaux dans les tests.

### Internationalisation (i18n)

- [ ] **`@angular/localize`** : Support officiel.
- [ ] **Internationalisation des messages dans les templates**.

### Server-Side Rendering (SSR)

- [ ] **Angular Universal vs. AnalogJS** : Comparaison des approches.
- [ ] **Hydratation partielle** : Amélioration de la performance perçue.
- [ ] **Prerendering (SSG)** : Génération statique de pages.

---

## 📚 4. Bibliothèques & Écosystème

### UI Component Libraries

- [ ] **Angular Material** : La bibliothèque officielle, avec Material 3.
  - [ ] Composants Material Design.
  - [ ] CDK (Component Dev Kit) : Utilitaires sans style.
- [ ] **PrimeNG** : Très complète, avec 90+ composants.
- [ ] **Kendo UI for Angular** : Suite professionnelle (payante).
  - [ ] **Nouveautés 2026** : Composants "Smart" avec IA intégrée, recherche sémantique.
- [ ] **NG-ZORRO** : Implémentation Ant Design pour Angular.
- [ ] **Taiga UI** : Bibliothèque récente et performante.
- [ ] **NgBootstrap** : Composants Bootstrap.

### State Management

- [ ] **NgRx** : La référence pour les applications complexes.
  - [ ] **NgRx Signals** : Version basée sur les signals.
  - [ ] **Component Store** : Gestion d'état locale.
- [ ] **Elf** : Alternative moderne, basée sur les observables/signals.
- [ ] **Akita** : Une autre option mature.
- [ ] **NGXS** : Approche plus simple que NgRx.

### Formulaires

- [ ] **Formulaires réactifs** : Toujours valables, mais en transition vers Signal Forms.
- [ ] **Signal Forms (Angular 21+)** : Nouvelle approche.
- [ ] **NGX-Formly** : Générateur de formulaires basé sur JSON.

### Data Visualization

- [ ] **D3.js avec Angular** : Intégration classique.
- [ ] **ECharts / ngx-echarts** : Graphiques performants.
- [ ] **Highcharts / AG Grid** : Solutions professionnelles.

### Backend & API

- [ ] **AngularFire** : Firebase pour Angular.
- [ ] **Apollo Angular** : GraphQL.
- [ ] **TanStack Query (Angular Query)** : Gestion d'état serveur.

### Testing

- [ ] **Jasmine + Karma** : L'ancien standard (à éviter).
- [ ] **Jest** : Alternative populaire.
- [ ] **Vitest** : Nouveau standard recommandé.
- [ ] **Cypress / Playwright** : Tests E2E.

---

## ⚠️ 5. Ce qui Change / Ce qui Disparaît

### Déprécié (à ne plus utiliser)

- [ ] ❌ **`NgModule`** : Plus nécessaire pour les nouveaux développements.
- [ ] ❌ **Zone.js** : Remplacé par le mode zoneless.
- [ ] ❌ **`*ngIf`, `*ngFor`, `*ngSwitch`** : Supprimés depuis Angular 22.
- [ ] ❌ **`ChangeDetectionStrategy.Default`** : Renommé `Eager`, et `OnPush` est le défaut.
- [ ] ❌ **Karma** : Remplacé par Vitest.
- [ ] ❌ **Webpack** : Remplacé par esbuild/Vite.
- [ ] ❌ **Injection par constructeur** : Fonction `inject()` privilégiée.
- [ ] ❌ **`@ViewChild`/`@ContentChild` synchrones** : Remplacés par les versions signals.

### Évolutions majeures

- [ ] 🔄 **RxJS** : Toujours utile pour les flux complexes, mais plus pour l'état local.
- [ ] 🔄 **Formulaires réactifs** : Migrer progressivement vers Signal Forms.
- [ ] 🔄 **Lazy loading** : Toujours important, mais via `@defer` en plus du routing.

---

## 🗺️ 6. Roadmap 2026-2027

### Angular 22 (Mai 2026)

- [ ] **OnPush par défaut** : Changement majeur d'architecture.
- [ ] **Angular Aria** : Composants headless accessibles.
- [ ] **Sélecteurs optionnels (expérimental)**.

### Angular 23 (Novembre 2026)

- [ ] **Sélecteurs optionnels (stable)**.
- [ ] **Hydratation partielle avancée**.
- [ ] **Intégration Web Components améliorée**.

### Angular 24+ (2027)

- [ ] **Suppression complète de l'ancien système de détection de changement**.
- [ ] **Compilateur entièrement réécrit (pour mémoire)**.
- [ ] **Support natif des standards W3C** (Observable, etc.).

---

## 📺 7. Ressources pour la Veille

### YouTube (Incontournables)

| Chaîne                                                   | Spécialité                                                |
| -------------------------------------------------------- | --------------------------------------------------------- |
| **[Igor Sedov](https://youtube.com/@IgorSedov)**         | News ultra-rapides, analyses des nouvelles versions       |
| **[Joshua Morony](https://youtube.com/@JoshuaMorony)**   | Tutoriels approfondis sur Signals, Zoneless, architecture |
| **[Deborah Kurata](https://youtube.com/@DeborahKurata)** | Explications claires des fondamentaux et bonnes pratiques |
| **[Loïc Magnette](https://youtube.com/@LoicMagnette)**   | Conférences sur le futur d'Angular (en français)          |
| **[NgConf](https://youtube.com/@NgConf)**                | Conférences officielles                                   |
| **[Angularidades](https://youtube.com/@Angularidades)**  | Podcast en espagnol avec des GDEs                         |

### Experts à suivre (X/Twitter, LinkedIn, Blogs)

- **Minko Gechev** (Angular team lead)
- **Enea Jahollari** (GDE)
- **Emma Twersky** (Angular team)
- **Pawel Kozlowski** (Angular team)
- **Sandra Willford** (Angular team)
- **Mark Techson** (Angular team)

### Sites & Blogs

- **[Blog Angular officiel](https://blog.angular.dev)** : Source primaire.
- **[Angular Weekly](https://angularweekly.substack.com/)** : Newsletter hebdomadaire.
- **[This is Angular](https://dev.to/t/angular)** : Articles de la communauté.
- **[Angular University](https://angular-university.io/)** : Cours approfondis.

### Outils de veille

- **Suivre les releases GitHub** : [angular/angular](https://github.com/angular/angular/releases)
- **Angular RFCs** : [angular/angular/discussions/categories/rfc](https://github.com/angular/angular/discussions/categories/rfc)
- **Twitter/X Lists** : Créer une liste des experts ci-dessus.

---

## ✅ Ma Checklist de Compétences Angular 2026

### Niveau Débutant

- [ ] Comprendre les composants standalone
- [ ] Maîtriser `@if`, `@for`, `@switch`
- [ ] Créer et utiliser des `signal()`, `computed()`
- [ ] Utiliser `input()` et `output()`
- [ ] Naviguer avec le routeur
- [ ] Faire des requêtes HTTP avec `HttpClient`

### Niveau Intermédiaire

- [ ] Zoneless change detection
- [ ] `effect()` et gestion des effets secondaires
- [ ] `model()` pour le two-way binding
- [ ] `linkedSignal()`
- [ ] Signal Forms
- [ ] `@defer` avec différents triggers
- [ ] Tests avec Vitest

### Niveau Avancé

- [ ] Architecture modulaire sans NgModule
- [ ] Optimisation des performances (change detection, memoization)
- [ ] Création de bibliothèques de composants
- [ ] Intégration RxJS ↔ Signals complexe
- [ ] SSR avec hydratation partielle
- [ ] State management avancé (NgRx Signals, Elf)
- [ ] Participation aux RFCs et contribution

---

*Dernière mise à jour : Février 2026*
