# Project Structure

Before we start making changes to the code, lets get a lay of the land.

`public/` - This folder holds static assets that will be included in the final bundle. The content is placed root of the project, and its contents can be accessed by `/my-image.png`, for example.

`src/app` - The location of the majority of the components and content of the app.

`src/app/globals.css` - This is the root stylesheet, and should contain any CSS that is intended to be project-wide, such as utility classes, variables, and other foundational style choices. In this project, this is the file that imports Tailwind CSS.

`src/app/layout.tsx` - The root layout of the project. The root layout should include UI that will be sharted by all pages, as well as the root structure of the HTML document.

`src/app/page.ts` - The component that will be rendered at the `/` route of the application.