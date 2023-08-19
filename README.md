```
git remote add origin git@github.com:jozemario/mgh-nx-nextjs-workspace.git
git branch -M master
git push -u origin master


Setup seed project
--------------------------------------
nvm use 18
npm install -g nx
npx create-nx-workspace@latest

>  NX   Let's create a new workspace [https://nx.dev/getting-started/intro]

✔ Choose what to create                 · integrated

✔ What to create in the new workspace   · next
✔ Repository name                       · @mghcloud
✔ Application name                      · local-dev
✔ Default stylesheet format             · scss
✔ Enable distributed caching to make your CI faster · Yes

>  NX   Distributed caching via Nx Cloud has been enabled

In addition to the caching, Nx Cloud provides config-free distributed execution,
UI for viewing complex runs and GitHub integration. Learn more at https://nx.app

Your workspace is currently unclaimed. Run details from unclaimed workspaces can be viewed on cloud.nx.app by anyone
with the link. Claim your workspace at the following link to restrict access.

https://cloud.nx.app/orgs/workspace-setup?accessToken=ZTFjYWMzYjctMzRmYS00OTdjLWIyMGYtY2MyYjFiNmRhMGNkfHJlYWQtd3JpdGU=
nx g @nrwl/workspace:remove x-common-login-component --forceRemove

nx g @nrwl/next:lib x-login-component --publishable --importPath=@mghcloud/x-login-component

nx build local-dev
nx build x-login-component
nx serve local-dev --prod


When using Next.js in Nx, you get the out-of-the-box support for TypeScript, Cypress, and Jest. No need to configure anything: watch mode, source maps, and typings just work.

The Next.js plugin contains executors and generators for managing Next.js applications and libraries within an Nx workspace. It provides:

Scaffolding for creating, building, serving, linting, and testing Next.js applications.
Integration with building, serving, and exporting a Next.js application.
Integration with React libraries within the workspace.

```

```
Creating Applications
You can add a new application with the following:

nx g @nrwl/next:app my-new-app

Generating Libraries
Nx allows you to create libraries with just one command. Some reasons you might want to create a library include:

Share code between applications
Publish a package to be used outside the monorepo
Better visualize the architecture using nx graph
For more information on Nx libraries, see our documentation on Creating Libraries and Library Types.

To generate a new library run:


nx g @nrwl/next:lib my-new-lib
Generating Pages and Components
Nx also provides commands to quickly generate new pages and components for your application.


nx g @nrwl/next:page my-new-page --project=my-new-app

nx g @nrwl/next:component my-new-component --project=my-new-app
Above commands will add a new page my-new-page and a component my-new-component to my-new-app project respectively.

Nx generates components with tests by default. For pages, you can pass the --withTests option to generate tests under the specs folder.

Using Next.js
Serving Next.js Applications
You can run nx serve my-new-app to serve a Next.js application called my-new-app for development. This will start the dev server at http://localhost:4200.

To serve a Next.js application for production, add the --prod flag to the serve command:


nx serve my-new-app --prod
Using an Nx Library in your Application
You can import a library called my-new-lib in your application as follows.


apps/my-next-app/pages/index.tsx
```
```typescript jsx
import { MyNewLib } from '@<your nx workspace name>/my-new-lib';

export function Index() {
return (
<MyNewLib>
<p>The main content</p>
</MyNewLib>
);
}

export default Index;
```
```

Publishable libraries
For libraries intended to be built and published to a registry (e.g. npm) you can use the --publishable and --importPath options.


nx g @nrwl/next:lib my-new-lib --publishable --importPath=@happynrwl/ui-components
Testing Projects
You can run unit tests with:


nx test my-new-app
nx test my-new-lib
Replace my-new-app and my-new-lib with the name or the project you want to test. This command works for both applications and libraries.

You can also run E2E tests for applications:


nx e2e my-new-app-e2e
Replace my-new-app-e2e with the name or your project with -e2e appended.

Linting Projects
You can lint projects with:


nx lint my-new-app
nx lint my-new-lib
Replace my-new-app and my-new-lib with the name or the project you want to test. This command works for both applications and libraries.

Building Projects
Next.js applications can be build with:


nx build my-new-app
And if you generated a library with --buildable, then you can build a library as well:


nx build my-new-lib
After running a build, the output will be in the dist folder. You can customize the output folder by setting outputPath in the project's project.json file.

The library in dist is publishable to npm or a private registry.

Static HTML Export
Next.js applications can be statically exported with:


nx export my-new-app
```
```
GIT SUBMODULES

Step 1: Create a new git repository with submodules:
Let’s start by creating a new git repository and adding submodules.

git init
git submodule add https://github.com/nrwl/nx-example-sharedlib sharedlib
git submodule add https://github.com/nrwl/nx-example-workspace workspace
We can use git submodules to create a parent git repo composed of multiple child repos, which is exactly what we need. I won’t go into detail on how they work exactly. So if you aren’t familiar with them (and very few people are), read more here.https://git-scm.com/book/en/v2/Git-Tools-Submodules

Step 2: Set up yarn workspaces
Next, let’s create a package.json file at the root to configure yarn workspaces.

{
  "private": true,
  "workspaces": ["workspace", "sharedlib"]
}
-----------------

git submodule update --remote --merge
git submodule update --remote --rebase

If you forget the --rebase or --merge, Git will just update the submodule to whatever is on the server and reset your project to a detached HEAD state.

$ git submodule update --remote

If we commit in the main project and push it up without pushing the submodule changes up as well, other people who try to check out our changes are going to be in trouble since they will have no way to get the submodule changes that are depended on. Those changes will only exist on our local copy.

In order to make sure this doesn’t happen, you can ask Git to check that all your submodules have been pushed properly before pushing the main project. The git push command takes the --recurse-submodules argument which can be set to either “check” or “on-demand”. The “check” option will make push simply fail if any of the committed submodule changes haven’t been pushed.

$ git push --recurse-submodules=check
The following submodule paths contain changes that can
not be found on any remote:
  DbConnector

Please try

	git push --recurse-submodules=on-demand

or cd to the path and use

	git push

```
## Dev Notes

<details><summary> Development </summary>
<p>

###### setup seed project
```
--------------------------------------
nvm use 18
npm install -g yarn nx
npx create-nx-workspace@latest

✔ Where would you like to create your workspace? · scope-apps-name
✔ Which stack do you want to use? · none
✔ Package-based or integrated? · integrated
✔ Enable distributed caching to make your CI faster · No

yarn add -D @nx/react
yarn add -D @nx/node
--------------------------------------
```
###### add apps, libs, configs with generators
```
--------------------------------------
Apps
nx generate @nx/node:application scope-team-api-backend
nx generate @nx/react:app scope-team-admin-frontend
nx generate @nx/react:app scope-team-other-frontend
----
Nx library 
the --publishable option when generating a new Nx library if your intention is to distribute it outside the monorepo
One particularity when generating a library with --publishable is that it requires you to also provide an --importPath. Your import path is the actual scope of your distributable package (e.g.: @myorg/mylib) - which needs to be a valid npm package name.

nx generate @nx/react:library shared-components --publishable --importPath=@scope-apps-name/shared-components

----
Remove apps, libs
nx g @nx/workspace:remove shared-components
nx g @nx/workspace:remove cypress-commands
----
Nx Node Docker Options Schema.
nx generate setup-docker @nx/node:application
npx nx docker-build scope-team-api-backend
----
Generate a Micro-service with a Docker File
npx nx g @nx/node:app orders-api --docker
----
Add Tailwind to NX project

Breakpoint prefix	Minimum width	CSS
sm	640px	@media (min-width: 640px) { ... }
md	768px	@media (min-width: 768px) { ... }
lg	1024px	@media (min-width: 1024px) { ... }
xl	1280px	@media (min-width: 1280px) { ... }
2xl	1536px	@media (min-width: 1536px) { ... }

yarn add tailwindcss@latest postcss@latest autoprefixer@latest
yarn add @tailwindcss/typography
yarn add @tailwindcss/forms
nx g @nx/react:setup-tailwind --project=scope-team-admin-frontend
nx g @nx/react:setup-tailwind --project=scope-team-other-frontend

By specifying the postcssConfig option, the PostCSS and Tailwind configuration will be applied to all libraries used by the application as well.
Using library-specific configuration files
If your libraries have their own postcss.config.js and tailwind.config.js files then you should not use the postcssConfig option. Doing so will ignore the library-specific configuration and apply the application's configuration to everything.

nx g @nx/react:setup-tailwind --project=shared-components

----
 yarn add @headlessui/react @heroicons/react

----
State Management
Apollo is a shared cache. You can just do useQuery(GET_SETTINGS); in every component that needs that data - if it's already in the cache, nothing to be done. Otherwise it will get it.
No need to replicate that in redux - apollo is now your cache state manager while redux is there for all the other data.

redux toolkit
nx generate @nx/react:library store --publishable --importPath=@scope-apps-name/store

nx g @nx/react:redux --dry-run --name=admin --project=store
nx g @nx/react:redux --name=admin --project=store

apollo client(graphql)

yarn add apollo-boost @apollo/react-hooks graphql
yarn add -D @graphql-codegen/cli @graphql-codegen/typescript-operations @graphql-codegen/typescript-react-apollo
nx g @nx/react:library graphql --publishable --importPath=@scope-apps-name/graphql

Add a new task in project.json to run grapqhl code generator:

"create-script": {
    "executor": "nx:run-commands",
    "options": {
        "commands": [
          "mkdir -p apps/frontend/scripts",
          "touch apps/frontend/scripts/my-script.sh",
          "chmod +x apps/frontend/scripts/my-script.sh"
        ],
        "parallel": false
    }
}

nx run graphql:generate 
nx g component SetList --project=graphql --directory=lib/utils
nx g component SetForm --project=graphql --directory=lib/utils

Backend
yarn add --exact graphql-yoga


----
Development environment
git clone repo_url
cd scope-apps-name
nvm use 18
yarn or npm
----
Testing
yarn add --dev @nx/cypress 
nx generate @nx/js:library --name=cypress-commands --buildable=false --publishable --importPath=@scope-apps-name/cypress-commands
✔ Which unit test runner would you like to use? · jest
✔ Which bundler would you like to use to build the library? Choose 'none' to skip build setup. · tsc
Each Nx lib is already set up and configured to work well with TypeScript. There is a
tsconfig.json which is the entry level TypeScript config file and extends from the root-level tsconfig.base.json
tsconfig.lib.json which holds the library specific TypeScript configuration
tsconfig.spec.json which is mainly for Jest tests
To make Cypress types work, we need to add cypress and node to the types property of the compilerOptions in tsconfig.lib.json:

{
  "extends": "./tsconfig.json",
  "compilerOptions": {
    ...
    "types": ["cypress", "node"]
  },
  ...
}
 add import '@scope-apps-name/cypress-commands' to app-e2e/src/support/e2e.ts

nx e2e scope-team-admin-frontend-e2e
nx e2e scope-team-admin-frontend-e2e --watch
nx e2e scope-team-other-frontend-e2e
nx e2e scope-team-api-backend-e2e
nx test shared-components

nx run-many -t e2e
nx run-many -t test
----
Serve apps
nx serve scope-team-admin-frontend
nx serve scope-team-admin-frontend --prod
nx serve scope-team-other-frontend
nx serve scope-team-api-backend
----
nx build scope-team-admin-frontend --prod
nx build scope-team-other-frontend --prod
nx build scope-team-api-backend --prod
--------------------------------------
```
###### add components

```
--------------------------------------
Generate a component in the shared-components library:
nx g @nx/react:component ...
nx g component sideBar --project=shared-components
nx g component contentView --project=shared-components
nx g component callToAction --project=shared-components
nx g component navBar --project=shared-components
nx g component baseLayout --project=shared-components --directory=lib/layouts
nx g component sidebarLayout --project=shared-components --directory=lib/layouts
nx g component dashboard --project=shared-components --directory=lib/views
nx g component locale --project=shared-components --directory=lib/utils
nx g component constant --project=shared-components --directory=lib/utils

nx g component appLogo --project=shared-components --directory=lib/common
nx g component appRoutes --project=scope-team-admin-frontend
--------------------------------------
```

</p>
</details>
