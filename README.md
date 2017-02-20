# ENSE471 - Vue.js Documentation Browser
A basic prototype of a user interface for a documentation browser made using [Vue.js](https://vuejs.org/) and some other libraries.  
This project was made with the sole intent of studying a student-chosen user interface library.

Have a look at the final product at <http://shevtsod.github.io/ENSE471docbrowser>

The current build of the project is simply a client-side user interface in the form of an SPA with a preloaded markdown document that can be edited by the user. Changes are lost upon reloading or closing the page.

## Build Instructions
To build the project, you should have [Node.js](https://nodejs.org/en/) installed.  
*   Clone this repository, and navigate to it on a command prompt using

```bash
cd directory-name
```  
*   In the root directory of the project, run the following command to install all of the dependencies of the project (apart from the static ones that are already provided under the `static/` directory).

```bash
npm install
```   
*   Finally, run one of the following:

``` bash
# Development build with hot reload at localhost:8080
npm run dev

# Production build with minification
npm run build
```

For a detailed explanation on the project's scaffold, please see the [docs for vue-loader](http://vuejs.github.io/vue-loader).

## Known Issues
*   There are several layout issues due to unfamiliary and difficulty in working with CSS flexbox.

## Credits
Below is a list of libraries used by this project:
*   [**Vue.js**](https://vuejs.org/)
*   [vue-loader](https://github.com/vuejs/vue-loader)
*   [webpack module bundler](https://webpack.github.io/)
*   [ES2015 by Babel](https://babeljs.io/)
*   [Sass](http://sass-lang.com/)
*   [Normalize.css](https://necolas.github.io/normalize.css/)
*   [Pug](https://pugjs.org/api/getting-started.html)
*   [Bootstrap](http://getbootstrap.com/)
*   [jQuery](https://jquery.com/)
*   [Font Awesome](http://fontawesome.io/)
*   [Showdown](https://github.com/showdownjs/showdown)
