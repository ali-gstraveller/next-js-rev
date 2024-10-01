                                        Chapter 1 

https://nextjs.org/learn/dashboard-app/getting-started

                                    Getting Started

                                Creating a new project

We recommend using pnpm as your package manager, as it's faster and more efficient than npm or yarn. If you don't have pnpm installed, you can install it globally by running:

npm install -g pnpm

To create a Next.js app, open your terminal, cd into the folder you'd like to keep your project, and run the following command:

npx create-next-app@latest nextjs-dashboard --example "https://github.com/vercel/next-learn/tree/main/dashboard/starter-example" --use-pnpm

This command uses create-next-app, a Command Line Interface (CLI) tool that sets up a Next.js application for you. In the command above, you're also using the --example flag with the starter example for this course.

                                Exploring the project

After installation, open the project in your code editor and navigate to nextjs-dashboard.

cd nextjs-dashboard

/app: Contains all the routes, components, and logic for your application, this is where you'll be mostly working from.

/app/lib: Contains functions used in your application, such as reusable utility functions and data fetching functions.

/app/ui: Contains all the UI components for your application, such as cards, tables, and forms. To save time, we've pre-styled these components for you.

/public: Contains all the static assets for your application, such as images.

Config Files: You'll also notice config files such as next.config.js at the root of your application. Most of these files are created and pre-configured when you start a new project using create-next-app. You will not need to modify them in this course.

                                        Placeholder data

For this project, we've provided some placeholder data in app/lib/placeholder-data.ts. Each JavaScript object in the file represents a table in your database. For example, for the invoices table:

                                        TypeScript

For now, take a look at the /app/lib/definitions.ts file. Here, we manually define the types that will be returned from the database. For example, the invoices table has the following types:


/app/lib/definitions.ts

export type Invoice = {
  id: string;
  customer_id: string;
  amount: number;
  date: string;
  // In TypeScript, this is called a string union type.
  // It means that the "status" property can only be one of the two strings: 'pending' or 'paid'.
  status: 'pending' | 'paid';
};

By using TypeScript, you can ensure you don't accidentally pass the wrong data format to your components or database, like passing a string instead of a number to invoice amount.

                                    Running the development server

Run pnpm i to install the project's packages.

pnpm i

Followed by pnpm dev to start the development server.

pnpm dev

                                    Chapter 2

https://nextjs.org/learn/dashboard-app/css-styling

                                    CSS Styling

                                    Global styles

Add global styles to your application by navigating to /app/layout.tsx and importing the global.css file:

/app/layout.tsx

import '@/app/ui/global.css'

If you take a look inside global.css, you'll notice some @tailwind directives:

/app/ui/global.css

@tailwind base;
@tailwind components;
@tailwind utilities;

                                        Tailwind

If you look at /app/page.tsx, you'll see that we're using Tailwind classes in the example.

                                        CSS Modules 

Inside /app/ui, create a new file called home.module.css and add the following CSS rules :

/app/ui/home.module.css

.shape {
  height: 0;
  width: 0;
  border-bottom: 30px solid black;
  border-left: 20px solid transparent;
  border-right: 20px solid transparent;
}

                                Using the clsx library to toggle class names

You can use clsx to conditionally apply the classes, like this:

/app/ui/invoices/status.tsx


https://nextjs.org/learn/dashboard-app/optimizing-fonts-images

                                        Chapter 3

                                    Optimizing Fonts and Images

                                Why optimize fonts?

Next.js automatically optimizes fonts in the application when you use the next/font module. It downloads font files at build time and hosts them with your other static assets. This means when a user visits your application, there are no additional network requests for fonts which would impact performance.

                                    Adding a primary font

1. In your /app/ui folder, create a new file called fonts.ts. You'll use this file to keep the fonts that will be used throughout your application.

/app/ui/fonts.ts

2. Import the Inter font from the next/font/google module - this will be your primary font. Then, specify what subset you'd like to load. In this case, 'latin':

3. Finally, add the font to the <body> element in /app/layout.tsx:

/app/layout.tsx

                                    Why optimize images?

1. Instead of manually implementing these optimizations, you can use the next/image component to automatically optimize your images.

                                  Adding the desktop hero image

1. In your /app/page.tsx file, import the component from next/image. Then, add the image under the comment:

https://nextjs.org/learn/dashboard-app/creating-layouts-and-pages

<Image
      src="/hero-desktop.png"
      width={1000}
      height={760}
      className="hidden md:block"
      alt="Screenshots of the dashboard project showing desktop version"
  />

https://nextjs.org/learn/dashboard-app/creating-layouts-and-pages

                                        Chapter 4

                                  Creating Layouts and Pages

                                Creating the dashboard page

1. Create a new folder called dashboard inside /app. Then, create a new page.tsx file inside the dashboard folder with the following content.

https://nextjs.org/learn/dashboard-app/navigating-between-pages

                                        Chapter 5

                                    Navigating Between Pages

                                      Why optimize navigation?

                                      The <Link> component

1. To use the <Link /> component, open /app/ui/dashboard/nav-links.tsx, and import the Link component from next/link. Then, replace the <a> tag with <Link>:

                                    Pattern: Showing active links

1. Since usePathname() is a hook, you'll need to turn nav-links.tsx into a Client Component. Add React's "use client" directive to the top of the file, then import usePathname() from next/navigation:

2. Next, assign the path to a variable called pathname inside your <NavLinks /> component:

3. Here's the final code for nav-links.tsx:

https://nextjs.org/learn/dashboard-app/setting-up-your-database#connect-and-deploy-your-project

                                  Setting Up Your Database





































































