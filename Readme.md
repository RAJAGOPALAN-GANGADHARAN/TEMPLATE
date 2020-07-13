# Steps to start a project

```sh
npm init
npm install express sequelize mysql2 body-parser cors --save
npx create-react-app frontend
npm install bootstrap axios react-router-dom
```

[Tutorial](https://bezkoder.com/node-js-express-sequelize-mysql/)

# Tips to Code

1. Create folder called app
2. Copy config and put into app
3. Create folders controllers, models,routes


> For Models
add file index.js -> will house and register all models here

```js
db.tutorials = require("./tutorial.model.js")(sequelize, Sequelize);
```

Create a model xxxx.model.js

```js
module.exports = (sequelize, Sequelize) => {
    const Tutorial = sequelize.define("tutorial", {
        title: {
            type: Sequelize.STRING
        },
        description: {
            type: Sequelize.STRING
        },
        published: {
            type: Sequelize.BOOLEAN
        }
    });

    return Tutorial;
};
```

> For Routes -> This will house all routers

```js
module.exports = app => {
    // Register your controller here ******IMPORTANT********
    const tutorials = require("../controllers/tutorial.controller.js");

    var router = require("express").Router();

    // Create a new Tutorial
    router.post("/", tutorials.create);

    // Retrieve all Tutorials
    router.get("/", tutorials.findAll);

    // Retrieve all published Tutorials
    router.get("/published", tutorials.findAllPublished);

    // Retrieve a single Tutorial with id
    router.get("/:id", tutorials.findOne);

    // Update a Tutorial with id
    router.put("/:id", tutorials.update);

    // Delete a Tutorial with id
    router.delete("/:id", tutorials.delete);

    // Create a new Tutorial
    router.delete("/", tutorials.deleteAll);

    /***** IMPORTANT UR URL Will be relative to this*******/
    app.use('/api/tutorials', router);
};
```

In server.js

```js
//below main get add ur route
require("./app/routes/tutorial.routes")(app);

//above port
const PORT=8080;
```


> For Controllers -> This will house all API endpoints behaviour a particular object

Create xxxx.controller.js

```js
/**** IMPORTANT FOR ALL NEW CONTROLLERS ****/
const db = require("../models");
const Tutorial = db.tutorials;
const Op = db.Sequelize.Op;
/****** YOUR LOGIC *****/

// Create and Save a new Tutorial
exports.create = (req, res) => {
  //req will have have a body use it to ur own way

};

// Retrieve all Tutorials from the database.
exports.findAll = (req, res) => {
  
};

// Find a single Tutorial with an id
exports.findOne = (req, res) => {
  
};

// Update a Tutorial by the id in the request
exports.update = (req, res) => {
  
};

// Delete a Tutorial with the specified id in the request
exports.delete = (req, res) => {
  
};

// Delete all Tutorials from the database.
exports.deleteAll = (req, res) => {
  
};

// Find all published Tutorials
exports.findAllPublished = (req, res) => {
  
};
```

> Frontend part

1. Copy src/App.js
2. Copy src/index.js