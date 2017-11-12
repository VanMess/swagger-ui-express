# Swagger UI Express

Adds middleware to your express app to serve the Swagger UI bound to your Swagger document. This acts as living documentation for your API hosted from within your app.

Updated to Swagger 3.4.4

## Usage

In app's `package.json`

    "swagger-ui-express": "latest" // or desired version

Express setup `app.js`
```javascript
const express = require('express');
const app = express();
const swaggerUi = require('swagger-ui-express');
const swaggerDocument = require('./swagger.json');

app.use('/api-docs', swaggerUi.serve, swaggerUi.setup(swaggerDocument));
```

Open http://`<app_host>`:`<app_port>`/api-docs in your browser to view the documentation.

If you want to set up routing based on the swagger document checkout [swagger-express-router](https://www.npmjs.com/package/swagger-express-router)

### [swagger-jsdoc](https://www.npmjs.com/package/swagger-jsdoc)

If you are using swagger-jsdoc simply pass the swaggerSpec into the setup function:

```javascript
// Initialize swagger-jsdoc -> returns validated swagger spec in json format
const swaggerSpec = swaggerJSDoc(options);

app.use('/api-docs', swaggerUi.serve, swaggerUi.setup(swaggerSpec));
```

### Swagger Explorer

By default the Swagger Explorer bar is hidden, to display it pass true as the second parameter to the setup function:

```javascript
const express = require('express');
const app = express();
const swaggerUi = require('swagger-ui-express');
const swaggerDocument = require('./swagger.json');

var showExplorer = true;

app.use('/api-docs', swaggerUi.serve, swaggerUi.setup(swaggerDocument, showExplorer));
```

### Custom swagger options

To pass custom options e.g. validatorUrl, to the SwaggerUi client pass an object as the third parameter:

```javascript
const express = require('express');
const app = express();
const swaggerUi = require('swagger-ui-express');
const swaggerDocument = require('./swagger.json');

var showExplorer = true;
var options = {
	validatorUrl : null
};

app.use('/api-docs', swaggerUi.serve, swaggerUi.setup(swaggerDocument, showExplorer, options));
```

### Custom CSS styles

To customize the style of the swagger page, you can pass custom CSS as the fourth parameter.

E.g. to hide the swagger header:

```javascript
const express = require('express');
const app = express();
const swaggerUi = require('swagger-ui-express');
const swaggerDocument = require('./swagger.json');

var showExplorer = false;
var options = {};
var customCss = '#header { display: none }';

app.use('/api-docs', swaggerUi.serve, swaggerUi.setup(swaggerDocument, showExplorer, options, customCss));
```

### Load swagger from url

To load your swagger from a url instead of injecting the document, pass `null` as the first parameter, and pass the relative or absolute URL as the sixth parameter.

```javascript
const express = require('express');
const app = express();
const swaggerUi = require('swagger-ui-express');

const swaggerDocument = require('./swagger.json');

app.static
app.use('/api-docs', swaggerUi.serve, swaggerUi.setup(null, null, null, null, null, 'http://petstore.swagger.io/v2/swagger.json'));
```

### Load swagger from yaml file

To load your swagger specification yaml file you need to use a module able to convert yaml to json ; for instance `yamljs`.

    npm install --save yamljs

```javascript
const express = require('express');
const app = express();
const swaggerUi = require('swagger-ui-express');
const YAML = require('yamljs');
const swaggerDocument = YAML.load('./swagger.yaml');

app.use('/api-docs', swaggerUi.serve, swaggerUi.setup(swaggerDocument));
```


## Requirements

* Node v0.10.32 or above
* Express 4 or above

## Testing

Install phantom
npm install
npm test
