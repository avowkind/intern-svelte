# Example Coding Challenge

This application demonstrates one solution to the coding challenge below. The challenge is to write a javascript web application that takes user entry data and makes API calls showing the results.

This version uses:

- [Svelte](https://svelte.dev/) - A JavaScript library for building user interfaces.

It is considerably lighter than the equivalent NextJS/React version.

The solution is a single page web app (SPA).

![Example App](/svelte-example.png)


## Application

The application is compiled by svelte into the public/index.html file and a bundle.js file. The whole package is 15k. ( yes 15k!)  

The main entry point is the `App` component. It is a Svelte component.

The page displays the EntryForm. When credentials are entered A GET request is made to the API to retrieve the user's data. The data are shown in the Repo Component. Data fetching is handled by plain browser fetch and does not take place until submit is clicked.

`getRepoDetails` is a function that takes the EntryForm values and sends a GET request to get the current Repo details. The data are then displayed in the Repo Component.

`updateRepoURL` is a function that takes the RepoForm url and calls the PATCH API to update the server record. It also calls the getRepoDetails function to revalidate the local data.

## Components

### Hero

    <Hero title='Title' />

A simple header component that accepts a `title` prop.

### Repo

    <Repo repo={data} />

A display box for a GitHub repository. Titled with the user's email address and annotated with the created and modified dates of the record. 


## Forms

### EntryForm

    <EntryForm initialValues={creds} onChange={setCreds} />

The EntryForm shows a form with text inputs for the user to enter their email address, and secret and a button to submit the form, both fields are required. The form is validated - checking the email address format. On Submit the form data is stored in the parent `creds` state.

The parent calls the API with the credentials to retrieve the current settings record - including the id field. The result is shown using the Repo component. If the API call fails an error is shown and the user is offered a Registration button to create a new record.

### RepoForm

    <RepoForm url={data.repoURL} onSubmit={handleSubmit} />

The Repo form shows a single text input for the user to enter the URL of the repository. The form is validated - checking the URL format. On Submit the form data is stored in the parent `data` state and then the PATCH API is called to update the record.


## Requirements

Your application must provide a GUI that allows a registered user to (without coding):

- Enter their email address and secret at the start of a session
- Modify their repository URL associated with their email address multiple times in the session.
- Confirm that their URL has been modified

You are welcome to use a tool like Postman to experiment with the API, but be aware that you need to finish working two hours after you register.

You may like to:

- Incorporate your name somewhere in the UI of the application
- Structure your code well and comment it where appropriate – we will look at it if your application seems to work.
- Let the user query the elapsed time since they registered and the date that the registration was last modified
- Query the repository URL currently registered for their email address
- Let the user register themselves initially through the application (it’s optional)
- Style the GUI in a way that is tasteful and clear and helpful to the user

Please do not:

- Get someone else to write the application for you – if you are interviewed we will ask you to talk us through your code and your design decisions.

## API  

### 1. To submit the URL of your code

PATCH to the URL <https://tweakplan.com/JavaScriptDemoSubmission-1.0/candidates/:id>
(use the "id for subsequent calls" above in the URL)

Put the JSON
{"repoURL":"{the URL of your git repository}","secret":"{your secret}"}

in the body of the request.
repoURL: this is the URL of a public code repository containg your JavaScript client
Example PATCH body
{"repoURL":"https://github.com/goldleaf/alpha","secret":" Split the atom "}

You can call this endpoint as many times as you like.

It will return the updated details and update the “last modified” time each time.

### 2. To confirm that everything has registered as intended

GET https://<same URL>/candidates?email=<your email address>&secret=<your secret>

You can call this as many times as you like.

It will return the updated details without changing the “last modified” time.

You can use it to retrieve your id number, or to check that you have succeeded in updating your repository URL.



# svelte app

This is a project template for [Svelte](https://svelte.dev) apps. It lives at https://github.com/sveltejs/template.

To create a new project based on this template using [degit](https://github.com/Rich-Harris/degit):

```bash
npx degit sveltejs/template svelte-app
cd svelte-app
```

*Note that you will need to have [Node.js](https://nodejs.org) installed.*


## Get started

Install the dependencies...

```bash
cd svelte-app
npm install
```

...then start [Rollup](https://rollupjs.org):

```bash
npm run dev
```

Navigate to [localhost:5000](http://localhost:5000). You should see your app running. Edit a component file in `src`, save it, and reload the page to see your changes.

By default, the server will only respond to requests from localhost. To allow connections from other computers, edit the `sirv` commands in package.json to include the option `--host 0.0.0.0`.

If you're using [Visual Studio Code](https://code.visualstudio.com/) we recommend installing the official extension [Svelte for VS Code](https://marketplace.visualstudio.com/items?itemName=svelte.svelte-vscode). If you are using other editors you may need to install a plugin in order to get syntax highlighting and intellisense.

## Building and running in production mode

To create an optimised version of the app:

```bash
npm run build
```

You can run the newly built app with `npm run start`. This uses [sirv](https://github.com/lukeed/sirv), which is included in your package.json's `dependencies` so that the app will work when you deploy to platforms like [Heroku](https://heroku.com).


## Single-page app mode

By default, sirv will only respond to requests that match files in `public`. This is to maximise compatibility with static fileservers, allowing you to deploy your app anywhere.

If you're building a single-page app (SPA) with multiple routes, sirv needs to be able to respond to requests for *any* path. You can make it so by editing the `"start"` command in package.json:

```js
"start": "sirv public --single"
```

## Using TypeScript

This template comes with a script to set up a TypeScript development environment, you can run it immediately after cloning the template with:

```bash
node scripts/setupTypeScript.js
```

Or remove the script via:

```bash
rm scripts/setupTypeScript.js
```

If you want to use `baseUrl` or `path` aliases within your `tsconfig`, you need to set up `@rollup/plugin-alias` to tell Rollup to resolve the aliases. For more info, see [this StackOverflow question](https://stackoverflow.com/questions/63427935/setup-tsconfig-path-in-svelte).

## Deploying to the web

### With [Vercel](https://vercel.com)

Install `vercel` if you haven't already:

```bash
npm install -g vercel
```

Then, from within your project folder:

```bash
cd public
vercel deploy --name my-project
```

### With [surge](https://surge.sh/)

Install `surge` if you haven't already:

```bash
npm install -g surge
```

Then, from within your project folder:

```bash
npm run build
surge public my-project.surge.sh
```
