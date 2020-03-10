# keyfrontend

## Project setup
```
yarn install
```

### Compiles and hot-reloads for development
```
yarn run serve
```

### Compiles and minifies for production
```
yarn run build
```

### Run your tests
```
yarn run test
```

### Lints and fixes files
```
yarn run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).


# Deployment on heroku

### npm install express --save


### Now add a server.js file to your project’s root directory:

> // server.js
    var express = require('express');
    var path = require('path');
    var serveStatic = require('serve-static');
    app = express();
    app.use(serveStatic(__dirname + "/dist"));
    var port = process.env.PORT || 5000;
    app.listen(port);
    console.log('server started '+ port);

### Build the application 

    npm run build

    The build shoud be located in the dist folder

    You can test it by first installing a library like serve

    npm install -g serve

    serve -s dist

### Follow Build Guide at Heroku.com

[href="https://devcenter.heroku.com/articles/deploying-nodejs" title="Build Guide"]


### If everything goes well you should have a url with a .herokuapp.com

This application was deployed to this url.
### https://ultimate-generator-frontend.herokuapp.com/