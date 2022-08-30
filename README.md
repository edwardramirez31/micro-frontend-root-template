# React Micro Frontend Template

## Getting Started

1. Run the script to initialize the project and install dependencies:

```bash
./setup.sh
```

2. Execute `yarn start` to run locally

3. Add your micro frontend apps at `src/index.ejs`

```html
<script type="systemjs-importmap">
  {
    "imports": {
      "react": "https://cdn.jsdelivr.net/npm/react@16.13.0/umd/react.production.min.js",
      "react-dom": "https://cdn.jsdelivr.net/npm/react-dom@16.13.0/umd/react-dom.production.min.js",
      "single-spa": "https://cdn.jsdelivr.net/npm/single-spa@5.3.0/lib/system/single-spa.min.js",
      "@${PROJECT_NAME}/root-config": "//localhost:9000/${PROJECT_NAME}-root-config.js",
      "@${PROJECT_NAME}/{MICRO_FRONTEND_NAME}": "//localhost:${YOUR_PORT}/${PROJECT_NAME}-{MICRO_FRONTEND_NAME}.js"
    }
  }
</script>
```

4. Make sure you have the HTML element with ID where you will inject each micro frontend

```html
<div id="${YOUR_ELEMENT_ID}"></div>
```

5. Register your micro frontend apps at `${PROJECT_NAME}-root-config.ts`

```js
registerApplication(
  "${PROJECT_NAME}/{MICRO_FRONTEND_NAME}",
  () => System.import("${PROJECT_NAME}/{MICRO_FRONTEND_NAME}"),
  (location) => ${CODE_TO_VALIDATE_ROUTE_HERE}
);
// OR
registerApplication({
  name: "${PROJECT_NAME}/{MICRO_FRONTEND_NAME}",
  app: () => System.import("${PROJECT_NAME}/{MICRO_FRONTEND_NAME}"),
  activeWhen: ["/${YOUR_ROUTES}"],
});
```

## Important notes

- Maintain consistency for the project name (all micro service and root project should have the same project name)

- It's recommended to setup the micro frontend apps repositories from [this template](https://github.com/edwardramirez31/micro-frontend-template) to be consistent with project naming convention

- This repository uses Semantic Release. If you don't want to use it:
  - Remove the step at `.github` or the entire folder
  - Remove `.releaserc` file
  - Remove `@semantic-release/changelog`, `@semantic-release/git`, `semantic-release` from `package.json`
