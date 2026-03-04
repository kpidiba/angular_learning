### TEMPLATES

- https://therichpost.com/ 

- [The most popular admin dashboard based on Angular 9+ and Nebular.](https://akveo.github.io/ngx-admin/material) 

- https://themeselection.com/angular-material-admin-template-free/

- [Angular](https://angular.io/guide)

- [GitHub - trungvose/jira-clone-angular: A simplified Jira clone built with Angular, ng-zorro and Akita](https://github.com/trungvose/jira-clone-angular)

- [GitHub - akveo/ngx-admin: Customizable admin dashboard template based on Angular 10+](https://github.com/akveo/ngx-admin) 

- [GitHub - ng-matero/ng-matero: Angular Material admin dashboard template.](https://github.com/ng-matero/ng-matero) 

- https://akveo.github.io/ngx-admin/ 

- https://primeng.org/templates

- https://github.com/codedthemes/gradient-able-free-admin-template 

# 🚀 Angular – Complete Developer Guide

## 📌 Description

Angular (souvent appelé **Angular 2+**) est un framework **open-source** basé sur TypeScript et maintenu principalement par Google ainsi que par une large communauté.

Angular est une **réécriture complète** de AngularJS.  
Il permet de développer des applications web modernes, en particulier des **SPA (Single Page Applications)**.

### 🎯 Pourquoi Angular ?

- Architecture robuste et scalable

- Basé sur TypeScript (typage fort)

- CLI puissant

- Dependency Injection native

- Routing intégré

- Gestion avancée des formulaires

- Écosystème mature (RxJS, Angular Material, etc.)

Angular favorise une architecture proche du modèle Model-View-Controller (séparation des responsabilités).

---

# 📂 Table of Contents

- Installation

- Création de projet

- Architecture

- Components

- Directives

- Data Binding

- Services & Dependency Injection

- Routing

- Forms

- Pipes

- Guards

- RxJS

- Angular + Spring Boot

- Resources

- Templates

---

# ⚙️ Installation

### 1️⃣ Installer Node.js (via NVM recommandé)

```bash
nvm install latest
nvm use latest
```

### 2️⃣ Installer Angular CLI

```bash
npm install -g @angular/cli
```

### 3️⃣ Vérifier la version

```bash
ng version
```

📌 Versions officielles :

- [Versioning and releases • Angular](https://angular.dev/reference/releases)

- [Version compatibility • Angular](https://angular.dev/reference/versions)

- [https://update.angular.io/](https://update.angular.io/)

---

# 🏗️ Créer un Projet

```bash
ng new myProject
cd myProject
ng serve
```

Changer le port :

```bash
ng serve --port 3000
```

---

# 📁 Structure du Projet

```gcode
src/
 ├── app/
 ├── assets/
 ├── environments/
 ├── index.html
 ├── main.ts
 └── styles.css
```

### 📌 Détails importants

- **app/** → logique applicative

- **assets/** → images, fichiers statiques

- **environments/** → configuration dev/prod

- **main.ts** → point d’entrée

- **index.html** → page racine

---

# 🧱 Components

Un **component** = Template (HTML) + Style (CSS) + Logique (TS)

Créer un composant :

```bash
ng g c component-name
```

Convention selector :

```ts
selector: 'app-component-name'
```

---

# 🔄 Data Binding

### Interpolation

```html
{{ variable }}
```

### Property Binding

```html
<img [src]="imageUrl">
```

### Event Binding

```html
<button (click)="onClick()"></button>
```

### Two-Way Binding

```html
<input [(ngModel)]="username">
```

Importer :

```ts
FormsModule
```

---

# 🧩 Directives

## 🔹 Structural (* modifie le DOM)

- `*ngIf`

- `*ngFor`

- `*ngSwitch`

```html
<li *ngFor="let item of items">{{ item }}</li>
```

## 🔹 Attribute (modifie style/comportement)

- `ngClass`

- `ngStyle`

```html
<div [ngClass]="{'active': isActive}"></div>
```

---

# 🧪 Lifecycle Hooks

| Hook              | Usage                  |
| ----------------- | ---------------------- |
| `ngOnInit`        | Initialisation logique |
| `ngAfterViewInit` | Manipulation DOM       |
| `ngOnDestroy`     | Nettoyage              |

---

# 🔌 Services & Dependency Injection

Créer un service :

```bash
ng g s services/user
```

```ts
@Injectable({
  providedIn: 'root'
})
export class UserService {}
```

Injection :

```ts
constructor(private userService: UserService) {}
```

---

# 🛣️ Routing

Configurer les routes :

```ts
RouterModule.forRoot([
  { path: 'home', component: HomeComponent },
  { path: '**', component: NotFoundComponent }
])
```

Navigation :

```html
<a routerLink="/home"></a>
```

Programmatique :

```ts
this.router.navigate(['/home']);
```

---

# 🛡️ Guards

```bash
ng g guard services/auth
```

Types :

- CanActivate

- CanDeactivate

- CanLoad

- Resolve

----

# 📝 Forms

## Template-Driven

Simple et rapide.

## Reactive Forms (Recommandé pour projet complexe)

```ts
ReactiveFormsModule
```

```ts
this.form.get('name')?.valueChanges.subscribe();
```

### Custom Validator

```ts
export function noSpace(control: AbstractControl) {
  return control.value.includes(' ') ? { noSpace: true } : null;
}
```

---

# 🎨 Pipes

Exemples :

```html
{{ name | uppercase }}
{{ date | date:'short' }}
{{ price | currency:'EUR' }}
{{ data | json }}
```

Créer un pipe :

```bash
ng g pipe summary
```

Cela va créer automatiquement :

```gcode
src/app/summary.pipe.ts
```

### ✅ Version simple (limite de caractères)

```ts
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'summary'
})
export class SummaryPipe implements PipeTransform {

  transform(value: string, limit: number = 100, trail: string = '...'): string {
    if (!value) return '';

    if (value.length <= limit) {
      return value;
    }

    return value.substring(0, limit) + trail;
  }

}
```

---

# 🔄 RxJS

Angular utilise RxJS pour gérer l’asynchrone.

Concept clé : **Observable**

```ts
import { Observable } from 'rxjs';

const obs = new Observable(observer => {
  observer.next('Hello');
});
```

---

# ⚡ Angular Standalone

Angular permet désormais de créer des composants **sans NgModule**.

Migration :

```bash
ng g @angular/core:standalone
```

Avantages :

- Moins de boilerplate

- Architecture simplifiée

- Meilleure maintenabilité

---

# 🔥 Angular + Spring Boot

Intégration avec Spring Boot :

- REST API

- CORS configuration

- DTO

- JWT Authentication

- Interceptors Angular

- Spring Security

Bonnes pratiques :

- Utiliser DTO

- Implémenter JWT

- Séparer Frontend & Backend

- Utiliser interceptors pour token

---

# 📦 Useful Commands

```bash
ng g c component
ng g s service
ng g i interface
ng g guard auth
ng generate environments
```

# 🎓 Learning Resources

### YouTube

- Angular University

- ng-conf

- Joshua Morony

- Academind

- Monsterlessons Academy

- Zoaib Khan

### Documentation

- [https://angular.dev](https://angular.dev)

- [https://rxjs.dev](https://rxjs.dev)

---

# 🎨 Templates & UI

- https://primeng.org/templates

- https://github.com/trungvose/jira-clone-angular

- https://adminmart.com/templates/angular/

- https://angulartemplates.com/ 

- [GitHub - ColorlibHQ/AdminLTE: AdminLTE - Free admin dashboard template based on Bootstrap 5](https://github.com/ColorlibHQ/AdminLTE) 

- [Peof - Job Board & Hiring Angular 20 Template](https://preview.hibootstrap.com/peof-ng/?client_id=1472350688.1771891202&session_id=1771891202)

- [Daxa - Angular 20 Material Design Admin Dashboard Template + SSR](https://preview.hibootstrap.com/daxa-admin/)

- https://therichpost.com/

- https://htmlrev.com/

---

## YOUTUBE RESSOURCES

- [Zoaib Khan - YouTube](https://www.youtube.com/@ZoaibKhan)

- [Simon Dieny - Code Senior - YouTube](https://www.youtube.com/@codeursenior)

- [Monsterlessons Academy - YouTube](https://www.youtube.com/@MonsterlessonsAcademy)

- [Joshua Morony - YouTube](https://www.youtube.com/@JoshuaMorony)

- [ng-conf - YouTube](https://www.youtube.com/@ngconfonline)

- https://www.youtube.com/@DecodedFrontend

- [Angularistic - YouTube](https://www.youtube.com/@angularistic)

- [Angular University - YouTube](https://www.youtube.com/@AngularUniversity)

- https://dyma.fr/developer/list/chapters/core (Learning course)

- [Nihira Techiees - YouTube](https://www.youtube.com/@NihiraTechiees)

- [Academind - YouTube]([Academind - YouTube](https://www.youtube.com/@academind))

- [Sahosoft Solutions](https://www.youtube.com/@sahosoftsolutions2343)

- [OctAcademy - YouTube](https://www.youtube.com/@OctAcademy)

- [Arthur Lannelucq - YouTube](https://www.youtube.com/@ArthurLannelucq)

- [NG Poland Conf - YouTube](https://www.youtube.com/@ngPolandConf) (Angular Conf News Ng Poland Conf)

- [LEARNING PARTNER - YouTube](https://www.youtube.com/@LearningPartnerDigital) (Projects)

- [Let's Program - YouTube](https://www.youtube.com/@letsprogram30)

- [Gaëtan Rouziès | Angular Lead - YouTube](https://www.youtube.com/@GaetanRouzies) (French)

- [SimpleTech - YouTube](https://www.youtube.com/@SimpleTechProd)

# 🧠 Key Concepts to Master

- Components architecture

- Lazy Loading

- Signals

- Change Detection

- State Management (NgRx)

- Interceptors

- Guards

- Clean folder structure

---

# 🏁 Conclusion

Angular est un framework **enterprise-ready**, idéal pour :

- Applications administratives

- Applications bancaires

- Portails gouvernementaux

- Applications complexes (comme ton projet eDOS 😉)

Il offre :

✅ Structure  
✅ Sécurité  
✅ Scalabilité  
✅ Maintenabilité
