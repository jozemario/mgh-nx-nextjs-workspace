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
nx serve x-login-component --prod


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
