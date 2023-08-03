<h1> Autorização e Autenticação no Angular </h1>

<h2> Sumário </h2>

- [Autenticação do usuário](#autenticação-do-usuário)
  - [Utilização do Subject e Behavior Subject](#utilização-do-subject-e-behavior-subject)
- [Guardas de rotas](#guardas-de-rotas)
  - [Implementação dos guardas nas rotas](#implementação-dos-guardas-nas-rotas)
  - [Implementando Interceptor](#implementando-interceptor)
  - [Habilitando o Interceptors e o AuthGuard no root](#habilitando-o-interceptors-e-o-authguard-no-root)

## Autenticação do usuário

Para a autenticação do usuário, primeiro é criado um serviço de autenticação para centralizar o controle de autenticação do usuário em um único serviço. Utiliza-se o comando `ng generate service common/auth/service/authentication`

```bash
ng generate service common/auth/service/authentication
```

### Utilização do Subject e Behavior Subject

Usa-se subjects para armazenar o estado atual do usuário e se ele está logado ou não, para permanecer esse estado em torno da aplicação

> `Subject` e `BehaviorSubject`: Sua funcionalidade é parecida com a de um observable (que é singlecast), só que pode ser direcionado a vários Observers (multicast)

Além disso usa-se o `Session Storage` do navegador para armazenar o token de acesso (geralmente JWT) do usuário, e cria-se os métodos de **login**, **logout**, **getUser** e **isUserLoggedIn**

- Model do Login

```ts
// app/common/auth/models/login.ts
interface Login {
  email: string;
  password: string;
}
```

- Serviço de **autenticação**

```ts
// app/common/auth/service/authentication.service.ts
@Injectable({
  providedIn: "root",
})
export class AuthenticationService extends HttpBaseService {
  private subjectUser: BehaviorSubject<any> = new BehaviorSubject(null);
  private subjectLogin: BehaviorSubject<any> = new BehaviorSubject(false);

  constructor(protected override readonly injector: Injector) {
    super(injector);
  }

  login(login: Login): Observable<any> {
    return this.httpPost<any>("authentication", login).pipe(
      map((response) => {
        sessionStorage.setItem("token", response.token);
        this.subjectUser.next(response.user);
        this.subjectLogin.next(true);

        return response.user;
      })
    );
  }

  logout() {
    sessionStorage.removeItem("token");
    this.subjectUser.next(null);
    this.subjectLogin.next(false);
  }

  isUserLoggedIn(): Observable<any> {
    const token = sessionStorage.getItem("token");
    if (token) {
      this.subjectLogin.next(true);
    }
    return this.subjectLogin.asObservable();
  }

  getUser(): Observable<any> {
    return this.subjectUser.asObservable();
  }
}
```

## Guardas de rotas

É utilizado para permitir ou negar o acesso em determinadas rotas da aplicação Angular pelo usuário. Através de guardas é possível usar as seguintes guardas de rotas:

- `CanActivate`: Verificar se a rota pode ser ativada
- `CanLoad`: Verificar se a rota pode ser carregada pelo browser
- `CanDeactivate`: Usado quando o usuário vai deslogar e ocorre o processo de perguntar para ele se ele irá descartar as alterações feitas
- `Interceptors`: usado quando fizer uma requisição, interceptar essa requisição e na requisição interceptada é adicionada o token

- Guarda de **autorização**

```ts
// app/common/auth/guards/auth.guard.ts
@Injectable({
  providedIn: "root",
})
export class AuthGuard implements CanActivate {
  constructor(
    private authenticationService: AuthenticationService,
    private router: Router,
  ) {}

  canActivate(
    route: ActivatedRouteSnapshot,
    state: RouterStateSnapshot
  ): Observable<boolean> {

    return this.authenticationService.isUserLoggedIn().pipe(
      tap((isLoggedIn) => {
        if (isLoggedIn == false) {
          this.router.navigateByUrl("/login");

          return false;
        } else {
          return true;
        }
      })
    );
  }
}
```

- Implementação do serviço **authenticationService** no componente de login (página de login)

```ts

@Component({
  selector: "app-login",
  templateUrl: "./login.component.html",
  styleUrls: ["./login.component.scss"],
})
export class LoginComponent implements OnInit {
  constructor(
    private authenticationService: AuthenticationService,
    private router: Router,
    private formBuilder: FormBuilder,
  ) {}

  loginForm!: FormGroup;
  authLogin!: Login;

  ngOnInit(): void {
    this.loginForm = this.formBuilder.group({
      email: ["", [Validators.required, Validators.email]],
      password: [
        "",
        Validators.compose([Validators.required, Validators.minLength(4)]),
      ],
    });
  }

  login() {
    this.authLogin = Object.assign({}, this.authLogin, this.loginForm.value);
    this.authenticationService.login(this.authLogin).subscribe(
      (user) => {
        if (user?.id) {
          this.router.navigateByUrl("dashboard");
        }
      },
    );
  }

  logout() {
    this.authenticationService.logout();
    this.router.navigate(["login"]);
  }
}
```

### Implementação dos guardas nas rotas

Para implementar nas rotas, basta adicionar o `AuthGuard` criado nas rotas, usando a propriedade `canActivate` nas rotas

```ts
// app-routing.module.ts
const routes: Routes = [
  { path: "", redirectTo: "dashboard", pathMatch: "full" },
  {
    path: "dashboard",
    loadChildren: () =>
      import("./features/dashboard/dashboard.module").then(
        (m) => m.DashboardModule
      ),
    canActivate: [AuthGuard],
  },
  {
    path: "login",
    loadChildren: () =>
      import("./common/auth/auth.module").then((m) => m.AuthModule),
  },
  { path: "**", component: PageNotFoundComponent },
];
// ...
```

### Implementando Interceptor

Usa-se interceptors para interceptar requisições HTTP e modifica-los de forma global (por exemplo adicionando um header) em cada requisição http feita

```ts
// app/common/auth/interceptor/auth.interceptor.ts
@Injectable()
export class AuthInterceptor implements HttpInterceptor {
  constructor() {}

  intercept(
    request: HttpRequest<any>,
    next: HttpHandler
  ): Observable<HttpEvent<any>> {
    const token = sessionStorage.getItem("token");
    let requestClone;

    if (token) {
      requestClone = request.clone({
        setHeaders: {
          // adicionar o token, por exemplo quando se usa JWT
          Authorization: `Bearer ${token}`,
        },
      });
    } else {
      requestClone = request;
    }

    return next.handle(requestClone);
  }
}
```

### Habilitando o Interceptors e o AuthGuard no root

```ts
// app.module.ts

@NgModule({
  declarations: [AppComponent, ToolbarComponent, PageNotFoundComponent],
  imports: [
    BrowserModule,
    AppRoutingModule,
    BrowserAnimationsModule,
    HttpClientModule,
    //...
  ],
  providers: [
    //...
    { provide: HTTP_INTERCEPTORS, useClass: AuthInterceptor, multi: true },
    AuthGuard,
  ],
  bootstrap: [AppComponent],
})
export class AppModule {}

```
