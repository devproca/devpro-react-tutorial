# Installation

There are multiple ways to use React, but the recommended approach is to use a framework.

Read the following to understand why "pure React" is no longer the standard approach: https://react.dev/learn/start-a-new-react-project#can-i-use-react-without-a-framework

In this tutorial, we will be using Next.js, but will be focusing on the aspects of React itself.

To get started, run the command:
```shell
npx create-next-app
```
> `npx` is a way of using a tool from npm without having to install it as a global or local dev package.

It will ask a series of questions about project setup:
```
✔ What is your project named? … devpro-react-tutorial
✔ Would you like to use TypeScript with this project? … No / [Yes]
✔ Would you like to use ESLint with this project? … No / [Yes]
✔ Would you like to use Tailwind CSS with this project? … No / [Yes]
✔ Would you like to use `src/` directory with this project? … No / [Yes]
✔ Use App Router (recommended)? … No / [Yes]
✔ Would you like to customize the default import alias? … [No] / Yes
```

Now we can start developing our app. Run `npm run dev` to start the app.

```
"dev": "next dev",
"build": "next build",
"start": "next start",
"lint": "next lint"
```