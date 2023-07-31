# Como criar um módulo para centralizar importações do Angular Material

- Basta criar um módulo utilizando o CLI do Angular
  - Utilize uma estrutura de pasta da forma que desejar

```bash
ng generate module shared/material/material
```

- Dentro do arquivo `app/shared/material/material.module.ts`

```ts
import { NgModule } from "@angular/core";
import { CommonModule } from "@angular/common";
import { MatCardModule } from "@angular/material/card";
import { MatSelectModule } from "@angular/material/select";
import { MatButtonModule } from "@angular/material/button";
import { MatToolbarModule } from "@angular/material/toolbar";
import { MatIconModule } from "@angular/material/icon";
import { MatFormFieldModule } from "@angular/material/form-field";
import { MatTableModule } from "@angular/material/table";
import { MatPaginatorModule } from "@angular/material/paginator";
import { MatInputModule } from "@angular/material/input";
import { FormsModule } from "@angular/forms";
import { MatDatepickerModule } from "@angular/material/datepicker";
import { MatNativeDateModule } from "@angular/material/core";
import { MatCheckboxModule } from "@angular/material/checkbox";
import { MatChipsModule } from "@angular/material/chips";
import { MatSnackBarModule } from "@angular/material/snack-bar";
import { MatMenuModule } from "@angular/material/menu";

@NgModule({
  declarations: [],
  imports: [
    CommonModule,
    MatCardModule,
    //... adicione os módulos dos componentes conforme for precisando

  ],
  exports: [
    MatCardModule,
    //... exporte os módulos dos componentes conforme for precisando
  ],
})
export class MaterialModule {}
```

- Depois, adicione o módulo criado `MaterialModule` nos módulos de roteamento conforme você ir desenvolvendo a aplicação

- Exemplo de um módulo de Dashboard (criado com a flag `--routing`)

```ts
import { NgModule } from "@angular/core";
import { CommonModule } from "@angular/common";

import { DashboardRoutingModule } from "./dashboard-routing.module";
import { DashboardComponent } from "./components/dashboard/dashboard.component";
import { MaterialModule } from "../../shared/material/material.module";

@NgModule({
  declarations: [DashboardComponent],
  imports: [
    CommonModule,
    DashboardRoutingModule,
    MaterialModule,
  ],
})
export class DashboardModule {}
```
