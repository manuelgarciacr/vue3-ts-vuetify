# vue3-ts-vuetify

## 1) Vue3 install

### Installing vue selecting manually the features

```
vue create project-name

Vue CLI v5.0.4

 (*) Babel
 (*) TypeScript
 (*) Progressive Web App (PWA) Support
 (*) Router
 (*) Vuex
 (*) CSS Pre-processors
 (*) Linter / Formatter
 (*) Unit Testing
 (*) E2E Testing
```

### Check the features needed for the project

```
? Choose a version of Vue.js that you want to start the project with 3.x
? Use class-style component syntax? Yes
? Use Babel alongside TypeScript (required for modern mode, auto-detected polyfills, transpiling JSX)? Yes
? Use history mode for router? (Requires proper server setup for index fallback in production) Yes
? Pick a CSS pre-processor (PostCSS, Autoprefixer and CSS Modules are supported by default): Sass/SCSS (with dart-sass)
? Pick a linter / formatter config: Basic
? Pick additional lint features: Lint on save
? Pick a unit testing solution: Jest
? Pick an E2E testing solution: Cypress
? Where do you prefer placing config for Babel, ESLint, etc.? In dedicated config 
```

## 2) Vue settings

### Configuring eslint to not warn about vue macros

```
// .eslintrc.js

module.exports = {
    ...,
    env: {
        ...,
        'vue/setup-compiler-macros': true
    },
    ...
}
```

## 3) Vuetify install

### Installing Vuetify selecting the Vuetify 3 Preview and the nightly build.

```
vue add vuetify

Choose a preset: Vuetify 3 Preview (Vuetify 3)
? Would you like to install Vuetify 3 nightly build? (WARNING: Nightly builds are intended for development testing and may include bugs or other issues.) Yes
```

## 4) Vuetify settings

### Avoid ts error: Cannot find module 'module-name' or its corresponding type declarations.ts(2307)

```
// src/shims-vuetify.d.ts

declare module 'vuetify'
declare module 'vuetify/lib/components'
declare module 'vuetify/lib/directives'
declare module 'vuetify/lib/util/colors'
declare module 'vuetify/lib/styles/generic'
...
```

### Adding custom properties and theme

```
// src/plugins/vuetify.ts

...
import colors from 'vuetify/lib/util/colors'

const light = {
    dark: false,
    colors: {
        background: '#FFFFFF',
        surface: '#FFFFFF',
        primary: colors.deepPurple.base,
        'primary-lighten-4': colors.deepPurple.lighten4,
        secondary: colors.teal.base,
        error: colors.red.base,
        info: colors.cyan.base,
        success: colors.green.base,
        warning: colors.amber.base,
    }
}

export default createVuetify({
    theme: {
        options: {
            customProperties: true,
        },
        variations: {
            colors: ['primary'],
            lighten: 2,
            darken: 2,
        },
        defaultTheme: 'light',
        themes: {
            light,
            dark: {
                dark: true,
                colors: {
                    primary: colors.red.darken1, // #E53935
                    secondary: colors.red.lighten4, // #FFCDD2
                    accent: colors.indigo.base, // #3F51B5
                }
            },
            ...
        },
        ...
    },
    ...
})
```

### Vuetify types in tsconfig

```
// tsconfig.json

{
    ...
    "compilerOptions": {
        ...
        "types": [
            ...
            "vuetify",
        ]
    }
}
```
