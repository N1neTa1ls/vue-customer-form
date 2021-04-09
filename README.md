# vue-customer-form

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).

### add project to github pages
create vue.config.js in params
module.exports = {
  publicPath: './'
  }
comment # /dist in gitignore file
and get this command at terminal
$ npm run build
$ git add dist && git commit -m "Initial dist subtree commit"
$ git subtree push --prefix dist origin gh-pages
