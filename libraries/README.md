# 📚 Angular Frontend Libraries (Enhanced Version)

Popular Angular libraries to improve UI, UX, and development productivity.

## ⭐ Main Libraries Covered

✅ Bootstrap (UI styling)  
✅ Angular Material (Modern UI components)  
✅ Toastr (Notifications)  
✅ SweetAlert2 (Dialogs & Alerts)  
✅ CKEditor (Rich text editing)  
✅ ApexCharts (Charts & analytics)

---

# 🎨 1. Bootstrap

### Installation

```bash
npm install bootstrap@5.2.3
```

### Configuration

Update **angular.json**

```json
"styles": [
  "node_modules/bootstrap/dist/css/bootstrap.min.css",
  "src/styles.scss"
],
"scripts": [
  "node_modules/bootstrap/dist/js/bootstrap.bundle.min.js"
]
```

> **Note:** Restart the server after making these changes. 

👉 Use Bootstrap mainly for:

- Quick layouts

- Responsive grids

- Utility styling

---

---

# 🎯 2. Angular Material (Recommended for Modern Angular Apps ⭐)

👉 Official Angular UI component library.

### Installation

```bash
ng add @angular/material
```

> **Material Icons**: You can access them from [Google Material Icons](https://fonts.google.com/icons). 

You will be prompted to choose:

- Theme

- Typography

- Animations

👉 Material Icons

```html
<link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
```

Use Material when you need:

- Professional enterprise UI

- Consistent design system

---

---

# ✨ 3. Toastr Notifications (ngx-toastr)

## Installation

```shell
npm install ngx-toastr @angular/animations
```

---

## Add Styles

In **angular.json**

```shell
"styles": [
  "node_modules/ngx-toastr/toastr.css",
  "src/styles.scss"
]
```

---

## Configure Module

### Module-based projects

```css
import { BrowserAnimationsModule } from '@angular/platform-browser/animations';
import { ToastrModule } from 'ngx-toastr';

@NgModule({
 imports: [
   BrowserAnimationsModule,
   ToastrModule.forRoot()
 ]
})
export class AppModule {}
```

---

### Standalone Angular (Modern approach ⭐)

If you are using Angular CLI, add the CSS to the `angular.json` file:

```json
bootstrapApplication(AppComponent, {
 providers: [
   provideAnimations(),
   provideToastr()
 ]
});
```

---

## Usage

```ts
constructor(private toastr: ToastrService) {}

showSuccess(){
 this.toastr.success('Operation completed');
}
```

---

# 🌟 4. SweetAlert2 (Modern Alert Modals)

## Installation



# Angular and SweetAlert2

**INSTALLATION** **<mark>(just install and use one)</mark>**

```bash
npm install sweetalert2 @sweetalert2/ngx-sweetalert2
```

### Module Setupts

```ts
import { SweetAlert2Module } from '@sweetalert2/ngx-sweetalert2';

@NgModule({
    //=> Basic usage (forRoot can also take options, see the wiki)
    imports: [SweetAlert2Module.forRoot()],

    //=> In submodules only:
    imports: [SweetAlert2Module],

    //=> In submodules only, overriding options from your root module:
    imports: [SweetAlert2Module.forChild({ /* options */ })]
})
export class AppModule {
}
```

That's it! By default, SweetAlert2 will be lazy-loaded, only when needed, from your local dependency of `sweetalert2`, using the `import()` syntax under the hood.

## 🔗 API

### `SwalDirective`

Add the `[swal]` attribute to an element to show a simple modal when that element is clicked.

To define the modal contents, you can pass a [`SweetAlertOptions` (provided by sweetalert2)](https://github.com/sweetalert2/sweetalert2/blob/main/sweetalert2.d.ts) object,
or a simple array of strings, of format `[title: string, text: string (, icon: string)]`.

A simple dialog:

```html
<button [swal]="['Oops!', 'This is not implemented yet :/', 'warning']">
  Do it!
</button>
```

More advanced, with text input, confirmation, denial and dismissal handling:

```html
<button
  [swal]="{ title: 'Save file as...', input: 'text', showDenyButton: true, denyButtonText: 'Don\'t save', showCancelButton: true }"  (confirm)="saveFile($event)"  (deny)="handleDenial()"  (dismiss)="handleDismiss($event)">

  Save
</button>
```

```ts
export class MyComponent {
  public saveFile(fileName: string): void {
    // ... save file
  }

  public handleDenial(): void {
      // ... don't save file and quit
  }

  public handleDismiss(dismissMethod: string): void {
    // dismissMethod can be 'cancel', 'overlay', 'close', and 'timer'
    // ... do something
  }
}
```

The directive can also take a reference to a [`<swal>` component](https://github.com/sweetalert2/ngx-sweetalert2#swalcomponent) for more advanced use cases:

```html
<button [swal]="deleteSwal" (confirm)="deleteFile(file)">
  Delete {{ file.name }}
</button>

<swal #deleteSwal title="Delete {{ file.name }}?" etc></swal>
```

### `SwalComponent`

The library also provides a component, that can be useful for advanced use cases, or when you `[swal]` has too many options.

The component also allows you to use Angular dynamic templates inside the SweetAlert (see the [`*swalPortal` directive](https://github.com/sweetalert2/ngx-sweetalert2#swalportaldirective) for that).

Simple example:

```html
<swal
  #deleteSwal
  title="Delete {{ file.name }}?"  text="This cannot be undone"  icon="question"  [showCancelButton]="true"  [focusCancel]="true"  (confirm)="deleteFile(file)">
</swal>

With [swal]:
<button [swal]="deleteSwal">Delete {{ file.name }}</button>

Or DIY:
<button (click)="deleteSwal.fire()">Delete {{ file.name }}</button>
```

You can access the dialog from your TypeScript code-behind like this:

```ts
class MyComponent {
  @ViewChild('deleteSwal')
  public readonly deleteSwal!: SwalComponent;
}
```

You can pass native SweetAlert2 options via the `swalOptions` input, just in the case you need that:

```html
<swal [swalOptions]="{ confirmButtonText: 'I understand' }"></swal>
```

By the way: every "special" option, like `swalOptions`, that are not native options from SweetAlert2,
are prefixed with `swal`.

You can catch other modal lifecycle events than (confirm), (deny) or (cancel):

```html
<swal
  (willOpen)="swalWillOpen($event)"  (didOpen)="swalDidOpen($event)"  (didRender)="swalDidRender($event)"  (willClose)="swalWillClose($event)"  (didClose)="swalDidClose()"  (didDestroy)="swalDidDestroy()">
</swal>
```

```ts
export class MyComponent {
    public swalWillOpen(event: WillOpenEvent): void {
      // Most events (those using $event in the example above) will let you access the modal native DOM node, like this:
      console.log(event.modalElement);
    }
}
```

## CKEDITOR

CKEditor is a powerful rich text editor that allows users to create and edit content with various formatting options, images, tables, and more. It is highly customizable and can be integrated into various web applications to provide a seamless content editing experience.

- **ROLE:** CKEditor serves as a rich text editor, enabling users to write and format content in a user-friendly interface. It is commonly used in content management systems, email clients, and other web applications where rich text editing is required

- **ALTERNATIVES :** summernote,tinyMCE

- **INSTALLATION PROCESS :** [Angular rich text editor component | CKEditor 5 documentation](https://ckeditor.com/docs/ckeditor5/latest/installation/integrations/angular.html)  

- **CUSTOM INTEGRATION: Go here Integrating a build from the online builder**

### 4. **ApexCharts** 📊

[ApexCharts](https://apexcharts.com/) is a modern charting library that helps you to create beautiful and interactive charts.

#### Installation:

```bash
npm install apexcharts ng-apexcharts --save
```

#### Configuration:

1. Import `NgApexchartsModule` into your Angular module:

```ts
import { NgApexchartsModule } from "ng-apexcharts";

@NgModule({
  imports: [
    NgApexchartsModule
  ]
})
export class AppModule { }
```

2. Use ApexCharts in your component:

```ts
import { Component } from '@angular/core';
import { ChartComponent } from "ng-apexcharts";

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  public chartOptions: any;

  constructor() {
    this.chartOptions = {
      chart: {
        type: 'line'
      },
      series: [{
        name: 'Sales',
        data: [30, 40, 35, 50, 49, 60, 70]
      }],
      xaxis: {
        categories: ['January', 'February', 'March', 'April', 'May', 'June', 'July']
      }
    };
  }
}
```

#### Usage Example (in Template):

```html
<apx-chart [series]="chartOptions.series" [chart]="chartOptions.chart" [xaxis]="chartOptions.xaxis"></apx-chart>
```
