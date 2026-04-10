# Angular Standalone Components

**The modern way to build Angular applications** — simpler, more tree-shakable, and fully lazy-loadable without `NgModule` boilerplate.

Since Angular 14 (preview) and 15 (stable), **standalone components** have become the recommended approach. Starting with **Angular 19**, `standalone: true` is the **default** — you no longer need to specify it explicitly in most cases.

## Why Standalone Components?

- **Simpler mental model**: Components are self-contained units.
- **Reduced boilerplate**: No more `declarations`, `imports`, or `exports` in `NgModule`s for every feature.
- **Better tree-shaking** and smaller bundles.
- **Easier lazy loading**: Use `loadComponent` directly on routes.
- **Incremental adoption**: Mix standalone components with existing `NgModule`-based code.
- **Future-proof**: The Angular team recommends standalone as the primary way to build apps.

**Goal**: Make Angular easier to learn and more enjoyable to use while keeping all its power.

## What is a Standalone Component?

A standalone component no longer needs to be declared in an `NgModule`. It declares its own dependencies directly via the `imports` array.

### Before (NgModule style)

```ts
// delia.component.ts
@Component({
  selector: 'app-delia',
  templateUrl: './delia.component.html'
})
export class DeliaComponent {}


// delia.module.ts
@NgModule({
  declarations: [DeliaComponent],
  imports: [CommonModule],
  exports: [DeliaComponent]   // if needed
})
export class DeliaModule {}
```

### After (Standalone — recommended)

```typescript
@Component({
  selector: 'app-delia',
  standalone: true,           // optional in Angular 19+
  imports: [
    CommonModule,
    RouterOutlet,
    MatButtonModule,
    AnotherStandaloneComponent   // you can import other standalone components too!
  ],
  templateUrl: './delia.component.html'
})
export class DeliaComponent {}
```

> You can also mark **directives** and **pipes** as standalone: true.

## Bootstrapping a Standalone Application

Delete app.module.ts and update main.ts:

```typescript
// main.ts
import { bootstrapApplication } from '@angular/platform-browser';
import { provideRouter } from '@angular/router';
import { provideHttpClient } from '@angular/common/http';
import { provideAnimations } from '@angular/platform-browser/animations';

import { AppComponent } from './app/app.component';
import { routes } from './app/app.routes';

bootstrapApplication(AppComponent, {
  providers: [
    provideRouter(routes),
    provideHttpClient(),
    provideAnimations(),
    // provideClientHydration() for SSR if needed
  ]
}).catch(err => console.error(err));
```

**Tip**: Many projects now use a separate app.config.ts for providers:

```typescript
// app.config.ts
export const appConfig: ApplicationConfig = {
  providers: [
    provideRouter(routes),
    provideHttpClient(),
    provideAnimations()
  ]
};

// main.ts
bootstrapApplication(AppComponent, appConfig);
```

## Routing & Lazy Loading (The Big Win)

No more loadChildren with modules. Use loadComponent for individual components or loadChildren for route groups.

### Basic Example (app.routes.ts)

```ts
import { Routes } from '@angular/router';

export const routes: Routes = [
  { path: '', redirectTo: 'home', pathMatch: 'full' },
  {
    path: 'home',
    loadComponent: () => import('./pages/home/home.component')
      .then(m => m.HomeComponent)
  },
  {
    path: 'admin',
    loadComponent: () => import('./admin/admin.component')
      .then(m => m.AdminComponent)
  },
  {
    path: '**',
    loadComponent: () => import('./pages/not-found/not-found.component')
      .then(m => m.NotFoundComponent)
  }
];
```

### Lazy Loading Child Routes

```typescript
// app.routes.ts
{
  path: 'pokemon',
  loadChildren: () => import('./pokemon/pokemon.routes')
    .then(m => m.POKEMON_ROUTES)
}
```

```typescript
// pokemon/pokemon.routes.ts
import { Routes } from '@angular/router';

export const POKEMON_ROUTES: Routes = [
  {
    path: '',
    loadComponent: () => import('./pokemon-list/pokemon-list.component')
      .then(m => m.PokemonListComponent)
  },
  {
    path: ':id/edit',
    loadComponent: () => import('./pokemon-edit/pokemon-edit.component')
      .then(m => m.PokemonEditComponent),
    canActivate: [AuthGuard]
  }
];
```

**Pro tip**: You can also provide services at the route level:

```typescript
{
  path: 'admin',
  providers: [AdminService],
  loadComponent: () => ...
}
```

## Generating Standalone Components

**New projects** (Angular 17+) are standalone by default.

For existing projects or specific components:

```bash
# Generate a standalone component
ng generate component card --standalone

# Or make all new components standalone by default (add to angular.json)
"schematics": {
  "@schematics/angular:component": {
    "standalone": true
  }
}
```

**Migration schematic** (highly recommended):

```bash
ng generate @angular/core:standalone
```

**Additional Good Practices**:

- Create a dedicated *.routes.ts file for every feature.
- Use provideRouter with functional guards, resolvers, and interceptors.
- Prefer provideHttpClient(withInterceptors([...])) over HttpClientModule.
- Keep AppComponent minimal — mostly <router-outlet></router-outlet>.
- Import only what you need in each component (IDE auto-import helps a lot).

**Example route naming convention**:

- pokemon.routes.ts
- admin.routes.ts
- dashboard.routes.ts

## Migrating an Existing App

1. Run the standalone migration schematic (see above).
2. Convert routing to use loadComponent / loadChildren.
3. Replace BrowserModule / BrowserAnimationsModule with providers (provideAnimations()).
4. Remove unused NgModule files gradually.
5. Test thoroughly — the migration is safe and incremental.

## Resources

- Official Angular Docs: [Standalone Components](https://angular.dev/guide/components/importing#standalone-components)
- Migration Guide: [angular.dev/reference/migrations/standalone](https://angular.dev/reference/migrations/standalone)
- Routing with Standalone: Angular Router documentation
- Video: Search for recent Angular standalone deep dives (2025–2026 content)
