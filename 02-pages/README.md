# 02. Pages in Next.js

- [02. Pages in Next.js](#02-pages-in-nextjs)
  - [Basic Pages](#basic-pages)
  - [Special Custom Pages](#special-custom-pages)

## Basic Pages

In Next.js, a **page** is a React component exported from a .js, .jsx, .ts, or .tsx file in the `pages` directory. Pages can also be added under `src/pages` as an alternative to the root pages directory.

**Note**: `src/pages` will be ignored if `pages` is present in the root directory.

> ✏ **Task**
>
> Open `src/pages/index.js` in your editor and replace the existing content with:
>
> ```jsx
> const Home = () => {
>   return (
>     <>
>       <header></header>
>       <main>
>         <h1>Welcome to my Next.js project</h1>
>       </main>
>       <footer>
>         Powered by <a href="https://nextjs.org">Next.js</a>
>       </footer>
>     </>
>   );
> };
>
> export default Home;
> ```
>
> Remove the useless imports in the file.
>
> If the Next.js development server is still running, as soon as you save the file, the browser automatically updates the page with the new content.

Next.js looks for the default homepage loading the `page/index.js`. The `index.js` file must contain one default exported function.

Each page is associated with a [**route**](../03-routing-and-navigation) based on its file name, so be careful to do not have other files or directories under pages that are not actual pages.

> ✏ **Task**
>
> Create a new file `src/pages/about.js` including a header, a main area and a footer section.
>
> Click to expand the file with the resolved task:
>
> <details>
>  <summary>📄 about.js</summary>
>
> ```jsx
> export default function About() {
>   return (
>     <>
>       <header></header>
>       <main>
>         <h1>About us</h1>
>         <h2>This is a starter Next.js project</h2>
>         <p>A hands-on laboratory to start working with Next.js</p>
>       </main>
>       <footer>
>         Powered by <a href="https://nextjs.org">Next.js</a>
>       </footer>
>     </>
>   );
> }
> ```
>
> </details>
>
> Navigate to <http://localhost:3000/about> in your development server to see the new page.

## Special Custom Pages

There are special pages in Next.js in the pages directory that are prefixed with the underscore symbol:

- `_app.js`. It is a custom component that Next.js uses to initialize pages.
- `_document.js`. It is a custom component that Next.js uses to augment the `<html>` and `<body>` tags in the application.

On the other hand, any file inside the folder `pages/api` is mapped to `/api/*` and will be treated as an API endpoint instead of a page.

In the next laboratories, we will use some of their features.

---

[<< **01**. Introducción a Next.js](../01-introduction) | [**03**. Routing and Navigation >>](../03-routing)
