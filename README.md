# Microfrontends - Next Steps in Modern UIs

Micro-frontend is a design pattern that extends the concepts of micro services to the frontend world. This is done by decomposing the frontend into individual, semi-independent **microapps**. 

## Why use a Microfrontend Setup

1. Technology Agnostic - Able to choose and upgrade stacks without coordinating with other teams. 
2. Decoupled Teams - Wither their isolated code and self-contained apps working on the same app.
3. Native Browser Features - using Browser Events for communication instead of building a global PubSub system. 
4. Resiliance and Consitency - Through a progressive app.

## implementation

All done through these splitting variants:
- Built-time split: micro apps are seperate npm pacakages, integrated into a parent component. Note that the parent needs to be rebuilt on every microapp change.
- Run-time split: Done through routing, and having the microapps as individual nodes loaded through javascript.

If you are an SRE kind of engineer, you see the potential of A/B testing and red/black deployments.

# Code it!

We will use a known framework called **single-spa** and build a runtime spit micro-frontend.

Create a root 'macro-app':

`npx create-single-spa --moduleType root-config --framework react --dir root`

Create a micro-app:

`npx create-single-spa --moduleType app-parcel  --framework react --dir micro`

Look at the package.json of the micro app, at the name - we will register this in our root app.

in the *index.ejs*, import our micro app:

```jsx
<script type="systemjs-importmap">
  {
    "imports": {
      "@single-spa/welcome": "https://unpkg.com/single-spa-welcome/dist/single-spa-welcome.js",
      "@radmada/root-config": "//localhost:9000/radmada-root-config.js",
      "react": "https://cdn.jsdelivr.net/npm/react@16.13.1/umd/react.production.min.js",
      "react-dom": "https://cdn.jsdelivr.net/npm/react-dom@16.13.1/umd/react-dom.production.min.js",
      "@radmada/radmada": "http://localhost:8080/radmada-radmada.js"
    }
  }
</script>
```

in the *microfrontend-layout.html*, register our micro app:
```jsx
<main>
  <route default>
    <application name="@radmada/radmada"></application>
  </route>
</main>
```

In the root, run:

`yarn start`

And there, we running microapps on a micro-frontend framework. We can register more micro-frontends to this root app.

## Start with React

We bootstrapped this project with [Create React App](https://github.com/facebook/create-react-app), or to summarise:

- `npm install -g create-react-app`
- `npx create-react-app mfe-app --template typescript`
- `yarn add react-router-dom`
- `yarn add typescript @types/node @types/react @types/react-dom @types/jest`
- `yarn start`

## Build, Deploy and Run

- `npm start` - Runs the app in the development mode on [http://localhost:3000](http://localhost:3000).
- `npm test`- Launches a test runner, see [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.
- `npm run build` - Builds the app for production to the `build` folder. See [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

## Further Documentation

- Code Splitting: [https://facebook.github.io/create-react-app/docs/code-splitting](https://facebook.github.io/create-react-app/docs/code-splitting)
- Analyzing the Bundle Size: [https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size](https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size)
- Making a Progressive Web App: [https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app](https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app)
- Advanced Configuration: [https://facebook.github.io/create-react-app/docs/advanced-configuration](https://facebook.github.io/create-react-app/docs/advanced-configuration)