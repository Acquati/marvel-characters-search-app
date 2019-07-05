# Marvel Characters Search

Search the most diverse characters on Marvel Universe.

![Site Screenshot](https://res.cloudinary.com/acquati/image/upload/v1562295452/marvel/github_jtwzz2.png)

## Tools

- [Vue](https://vuejs.org/)
- [Vuetify](https://vuetifyjs.com/en/)
- [Nuxt](https://nuxtjs.org/)
- [Google Cloud](https://cloud.google.com/)
- [Marvel Developer](https://developer.marvel.com/)

## Build Setup

``` bash
# install dependencies
$ yarn install

# serve with hot reload at localhost:3000
$ yarn run dev

# build for production and launch server
$ yarn run build
$ yarn start

# generate static project
$ yarn run generate
```

### VSCode

Use this configurations on your settings.json for ESLint and Prettier.

```json
{
  "eslint.validate": [
      {
        "language": "vue",
        "autoFix": true
      },
      {
        "language": "javascript",
        "autoFix": true
      },
      {
        "language": "javascriptreact",
        "autoFix": true
      }
    ],
  "eslint.autoFixOnSave": true,
  "editor.formatOnSave": false,
  "vetur.validation.template": false,
  "[javascript]": {
    "editor.defaultFormatter": "vscode.typescript-language-features"
  },
  "[html]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  }
}
```
