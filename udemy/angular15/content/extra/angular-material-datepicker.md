# Como Implementar o Componente de DatePicker traduzido em PT-BR

Basta adicionar no módulo `root` (`app.module.ts`) o seguinte trecho de código:

```ts
import { LOCALE_ID } from "@angular/core";
import localePt from "@angular/common/locales/pt";
import { registerLocaleData } from "@angular/common";

registerLocaleData(localePt);

@NgModule({
  declarations: [AppComponent, ToolbarComponent, PageNotFoundComponent],
  imports: [
    BrowserModule,
    //...
  ],
  providers: [
    { provide: LOCALE_ID, useValue: "pt-BR" },
  ],
  bootstrap: [AppComponent],
})
export class AppModule {}
```

- Template de um componente normal com o date picker:

```html
  <mat-form-field>
    <mat-label>Selecione uma data</mat-label>
    <input matInput [matDatepicker]="picker" />
    <mat-datepicker-toggle
      matIconSuffix
      [for]="picker"
    ></mat-datepicker-toggle>
    <mat-datepicker #picker></mat-datepicker>
  </mat-form-field>
```
