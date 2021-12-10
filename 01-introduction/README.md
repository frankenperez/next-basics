# 01. Introduction to Next.js

- [01. Introduction to Next.js](#01-introduction-to-nextjs)
  - [What is Next.js](#what-is-nextjs)
  - [Main features of Next.js](#main-features-of-nextjs)
  - [Installation](#installation)
  - [Next.js application structure](#nextjs-application-structure)
  - [Linters and Formatters](#linters-and-formatters)
    - [ESLint](#eslint)
    - [Prettier](#prettier)

## What is Next.js

[**Next.js**](https://nextjs.org/) is an **open-source React front-end development web framework** created by Vercel that enables functionality such as server-side rendering and generating static websites for React based web applications. It is a production-ready framework that allows developers to quickly create **static and dynamic [Jamstack](#-additional-concepts) websites**.

Next.js is an integral part of the React ecosystem developed specifically to address the SSR/SSG challenge for React applications and supports IE11 and all modern browsers.

## Main features of Next.js

- **Image Optimization**. `<Image>` and Automatic Image Optimization with instant builds.
- **Internationalization**. Built-in Domain & Subdomain Routing and Automatic Language detection.
- **Next.js Analytics**. A true lighthouse score based on real visitor data & page-by-page insights
- **Zero Config**. Automatic compilation and bundling. Optimized for production from the start.
- **Hybrid: SSG and SSR**. Pre-render pages at build time (SSG) or request time (SSR) in a single project.
- **Incremental Static Regeneration**. Add and update statically pre-rendered pages incrementally after build time.
- **TypeScript Support**. Automatic TypeScript configuration and compilation.
- **Fast Refresh**. Fast, reliable live-editing experience, as proven at Facebook scale.
- **File-system Routing** .Every component in the pages directory becomes a route.
- **API Routes**. Optionally create API endpoints to provide backend functionality.
- **Built-in CSS Support**. Create component-level styles with CSS modules. Built-in Sass support.
- **Code-splitting and Bundling**. Optimized bundle splitting algorithm created by the Google Chrome team.
- **Hot Reloading**. Application refresh is not needed in development mode. The idea behind hot reloading aka "hot module reloading" is to keep the app running and to inject new versions of the files that you edited at runtime without refresh the entire application.

## Installation

Next.js requires a **Node version 10.13 or later**.

> ✏ Install [Node](https://nodejs.org/), if it is not installed.

To easiest way to start a new Next.js project is to create it automatically by using `create-next-app`:

```bash
npx create-next-app
# or
yarn create next-app
```

There are several [options](https://nextjs.org/docs/api-reference/create-next-app) for configuring this initial app and many [official Next.js examples](https://github.com/vercel/next.js/tree/canary/examples) that can be used in place of the default template.

You also can setup manually by installing `react`, `react-dom` and `next`.

> ✏ **Task**
>
> Create a new root directory for the project. To follow the current example: `fruits-and-veggies`.
>
> Run `npx create-next-app` or `yarn create next-app`.
>
> Accept if you are asked to install the create-next-app package.
>
> Provide a project name when required. To follow this example: `next-app`.
>
> After the installation is complete, navigate to the `next-app` directory.
>
> Run `npm run dev` or `yarn dev` to start the development server on port 3000.
>
> Visit http://localhost:3000 to view your application.

Once the server is running, you should see a page like this one when you access http://localhost:3000:

![Next starter template](../../resources/images/lab01_home.png)

By using `create-react-app`, a list of scripts is available to facilitate application development at different stages:

- `next dev`. To start Next.js server in development mode.
- `next build`. To create an optimized production build of your application.
- `next start`. To start Next.js server in production mode. The application must be compiled with `next build` first.
- `next lint`. To set up ESLint if it is not already configured and check ESLint warnings or errors in the application.

## Next.js application structure

The package `create-next-app` creates a new Next.js application with the following folder structure:

```text
next-app
├── node_modules
├── pages
│   ├── api
│   │   └── hello.js
│   ├── _app.js
│   └── index.js
├── public
│   ├── favicon.ico
│   └── vercel.svg
├── styles
│   ├── global.css.ico
│   └── Home.module.css
├── .eslintrc.json
├── .gitignore
├── next.config.js
├── package-lock.json | yarn.lock
├── package.json
└── readme.md
```

When it comes to **structuring a Next.js application** the ideal folder organization is the one that allows you to move around your code with the least amount of effort, encouraging scalability but also reusability.

One common design pattern is to move app-related code to a new **src directory** and create other new directories to place React components, tests, custom hooks, interfaces, etc. depending on the needs. This approach is great for small projects because it makes it obvious where your files should be located and many developers are familiar with.

The src directory is supported by Next.js by default, but consider that config files like next.config.js should be inside the root directory and moving them to src won't work. The same goes for the public directory:

```text
next-app
├── node_modules
├── public
│   ├── favicon.ico
│   └── vercel.svg
├── src
│   ├── components
│   ├── hooks
│   ├── layouts
│   ├── pages
│   │   ├── api
│   │   │   └── hello.js
│   │   ├── _app.js
│   │   └── index.js
│   ├── services
│   ├── styles
│   │   ├── global.css.ico
│   │   └── Home.module.css
│   ├── test
│   └── utils
├── .eslintrc.json
├── .gitignore
├── next.config.js
├── package-lock.json | yarn.lock
├── package.json
└── readme.md
```

However, while it's great at the beginning, you'll realize at some point and depending on the size of your project that the main issue with this design is its lack of scalability. To solve this, we can refactor and group the code **by functional modules** instead of technical concepts and keep the dependencies between the modules to an absolute minimum. Code that is related to each other is grouped together in the `src/modules` directory and those that don't really fit in any module or that can be reused by the functional modules is moved to the `src/common` directory:

```text
next-app
├── node_modules
├── public
│   ├── favicon.ico
│   └── vercel.svg
├── src
│   ├── common
│   │   ├── components
│   │   ├── hooks
│   │   ├── layouts
│   │   ├── styles (or placed together with each component or layout)
│   │   ├── test (or placed together with each component or layout)
│   │   └── utils
│   ├── modules
│   │   ├── products
│   │   ├── users
│   │   └── ...
│   └── pages
│       └── index.js
├── .eslintrc.json
├── .gitignore
├── next.config.js
├── package-lock.json | yarn.lock
├── package.json
└── readme.md
```

> ✏ **Task**
>
> Because this is a small Next.js application, just for learning purposes and to keep it simple enough, we will use the first design pattern.
>
> Move the `pages` and `styles` folders and their content to a new `src` directory.
>
> ```text
> next-app
> ├── node_modules
> ├── public
> │   ├── favicon.ico
> │   └── vercel.svg
> ├── src
> │   ├── pages
> │   │    └── api
> │   │        └──hello.js
> │   │   ├── _app.js
> │   │   └── index.js
> │   └── styles
> │       ├── global.css.ico
> │       └── Home.module.css
> ├── .eslintrc.json
> ├── .gitignore
> ├── next.config.js
> ├── package-lock.json | yarn.lock
> ├── package.json
> └── readme.md
> ```
>
> If your development server is still running, visit http://localhost:3000 to check your application works.

## Linters and Formatters

### ESLint

Next.js provides an integrated [ESLint](https://eslint.org/) experience out of the box, automatically installing `eslint` and `eslint-config-next` as development dependencies in the application and creating an `.eslintrc.json` file in the root directory.

> ✏ **Task**
>
> Run `npm run lint` or `yarn lint` to set up ESLint if it was not already configured during the installation process.
>
> Open the `.eslintrc.json` file and update its configuration:
>
> ```json
> {
>   "extends": ["next/core-web-vitals"]
> }
> ```

### Prettier

[Prettier](https://prettier.io/) is an opinionated code formatter with support for many languages to enforce a consistent style by parsing the application code and re-printing it with its own rules.

ESLint contains code formatting rules which can conflict with the Prettier setup. It is recommended to include `eslint-config-prettier` in the ESLint config to make ESLint and Prettier work together, disabling any linting rule that might interfere with an existing Prettier rule, and `eslint-plugin-prettier` to run Prettier analysis as part of ESLint and reports differences as individual ESLint issues.

> ✏ **Task**
>
> Let’s add Prettier and the recommended plugins to work with ESLint:
>
> ```bash
> npm install -D prettier eslint-config-prettier eslint-plugin-prettier
> #or
> yarn add -D prettier eslint-config-prettier eslint-plugin-prettier
> ```
>
> Create a new file `.prettierrc` in the root directory to customize the configuration:
>
> ```json
> {
>   "printWidth": 100,
>   "tabWidth": 2,
>   "trailingComma": "none"
> }
> ```
>
> Open the `.eslintrc.json` file and update its configuration:
>
> ```json
> {
>   "extends": ["next/core-web-vitals", "prettier"]
> }
> ```
>
> Optionally, you can install the [Prettier Formatter extension](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode) for Visual Studio Code

---

[<< **00**. Key Concepts](../00-concepts) | [**02**. Pages in Next.js >>](../02-pages)
