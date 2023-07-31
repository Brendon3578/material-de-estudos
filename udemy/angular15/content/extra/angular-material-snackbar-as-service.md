# Como utilizar o Componente de SnackBar sendo um serviço reutilizável

- Primeiro crie um **serviço** chamado `SnackBar` em uma pasta (utilizando a estrutura de pasta que desejar) utilizando o CLI do Angular

```bash
ng generate service shared/material/snack-bar/snack-bar
```

- Depois basta injetar o `MatSnackBar` no serviço no `constructor` e criar um método que será utilizado na aplicação para chamar o SnackBar, tendo como argumento a mensagem que será exibida pelo SnackBar

```ts
import { Injectable } from "@angular/core";
import { MatSnackBar } from "@angular/material/snack-bar";

@Injectable({
  providedIn: "root",
})
export class SnackBarService {
  constructor(private matSnackBar: MatSnackBar) {}

  openSnackBar(message: string) {
    this.matSnackBar.open(message, "Fechar", {
      duration: 4000,
    });
  }
}
```

- Depois basta utilizar esse serviço criado no componente e utilizar o método `openSnackBar` quando for precisar chamar a snackBar
- Exemplo de utilização em uma toolbar

```ts
import { SnackBarService } from "../../../shared/material/snack-bar/snack-bar.service";

@Component({
  selector: "app-toolbar",
  templateUrl: "./toolbar.component.html",
  styleUrls: ["./toolbar.component.scss"],
})
export class ToolbarComponent {
  constructor(
    private snackBarService: SnackBarService,
    private router: Router
  ) {}
  
  logout() {
    this.router.navigate(["login"]).then(() => {
      this.snackBarService.openSnackBar("Desconectado com sucesso!");
    });
  }
}
```
