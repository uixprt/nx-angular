# NxWorkspace

This project was generated using [Nx](https://nx.dev).

The creation Progress is as follow:

1.  `nvm install stable`
2.  `npm install -g @angular/cli create-nx-workspace yarn nx`
3.  `create-nx-workspace nx-workspace --appName=nxWorkspace --preset=angular-nest --npmScope=ai --linter=eslint --style=scss --nx-cloud=false`
4.  `cd nx-workspace && yarn start`

    now we get an error in the console:

    ```
    [webpack-dev-server] [HPM] Error occurred while proxying request localhost:4200/api/hello to http://localhost:3333/ [ECONNREFUSED] (https://nodejs.org/api/errors.html#errors_common_system_errors)
    ```

    to solve this error:

5.  run: `yarn add -D concurrently`
6.  add this to root `package.json` scripts:

    ```json
        "start": "npm run serve:all",
        "serve:api": "nx run api:serve",
        "serve:web": "ng serve --open",
        "serve:all": "concurrently \"npm run serve:api\" \"npm run serve:web\"",
    ```

    now in the web page that opened you can see message: "welcome to api!"
    
    
    adding some npm libraries:

7.  `nx add @angular/material --defaults=true --interactive=false && nx add @ngrx/store --defaults=true --interactive=false`
8.  adding two interfaces to file `libs/api-interfaces/src/lib/api-interfaces.ts`

    ```ts
    export interface BaseEntity {
      id: string | null;
    }

    export interface Widget extends BaseEntity {
      title: string;
      description: string;
    }
    ```

    adding libs:

9.  `nx g lib core-data --parent-module=apps/dashboard/src/app/app.module.ts && nx g lib core-state --parent-module=apps/dashboard/src/app/app.module.ts && nx g lib material --parent-module=apps/dashboard/src/app/app.module.ts`

    generate a service:

10. `nx g s service/widgets/widgets --project=core-data`

    generate a routing module

11. `nx g m routing --flat=true -m=app.module.ts`

    generate some components:

12. `nx g c widgets -m app.module.ts --style=scss && nx g c widgets/widgets-list -m app.module.ts --style=scss && nx g c widgets/widget-details -m app.module.ts --style=scss`
13. `nx g c home -m app.module.ts --style=scss`
14. copy and paste [this](https://raw.githubusercontent.com/onehungrymind/fem-production-angular/main/libs/material/src/lib/material.module.ts 'form onehungrymind/fem-production-angular') in the same file

    if you are using VS Code here is an recommended extension: IntelliJ IDEA Keybindings by Keisuke Kato
    now you can use this with `ctrl + shift + a` to open run console: and run: `Organize Imports`, or `Sort Lines Ascending` on selected lines

### references:

- [Production-Grade Angular](https://frontendmasters.com/courses/production-angular/)
- [fem-production-angular](https://github.com/onehungrymind/fem-production-angular)
