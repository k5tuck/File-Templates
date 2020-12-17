# Copy Files

## Steps to make Express Server with All Requirements

### From Scratch

1.
2.
3.
4.
5.
6.
7.
8.
9.
10.

### Cloning this README

1.
2.
3.
4.
5.
6.
7.
8.
9.
10.

## NPM Dependencies

```
npm i express express-es6-template-engine morgan helmet dotenv sequelize pg pg-hstore express-session session-file-store bcryptjs
```

```
npm i --save-dev nodemon sequelize-cli
```

// Index.js (Main) - Parse Data from POST requests
app.use(express.urlencoded({extended: true}));

## Gitignore

```
node_modules
config
sessions
.env
```

## Session Files

// Needed Dependencies
express-session session-file-store

// Package.json

```
"nodemonConfig": {
"ignore": [
"sessions/*"
]
},
```

// Index.js (Main)

```
const session = require('express-session');
const FileStore = require('session-file-store')(session);
```

```
app.use(session({
store: new FileStore(), // store in files on the server
secret: process.env.SESSION_SECRET,
saveUninitialized: false,
resave: true,
rolling: true,
cookie: { // "magic band"
maxAge: 1000 * 60 * 60 * 24 * 7
}
}));
```

// Initializing Session

```
req.session.user = {
// username
// id: user ID from data table
}
```

// Authorization File (auth.js)

```
const requireLogin = (req, res, next) => {
    if (req.session.user) {
        next();
    } else {
        res.redirect('/unauthorized');
    }
}

module.exports = {
    requireLogin
};
```

## Dotenv Installation

Add .env to .gitignore

// Sequelizerc File (.sequelizerc)

```
'use strict';

require('dotenv').config();
const path = require('path');

module.exports = {
'config': path.resolve('config', 'config.js'),
'models-path': path.resolve('models'),
'seeders-path': path.resolve('seeders'),
'migrations-path': path.resolve('migrations'),
};
```

// dist.env

```
DB_USER=
DB_PASSWORD=
DB_NAME=
DB_HOST=
SESSION_SECRET=
```

Create copy of dist.env for .env
cp dist.env .env
paste in login information

// index.js (Main)

```
require('dotenv').config();
```

// Config.js

```
module.exports = {
  development: {
    username: process.env.DB_USER,
    password: process.env.DB_PASSWORD,
    database: process.env.DB_NAME,
        host: process.env.DB_HOST,
    dialect: 'postgres',
  }
};
```

In config file change config.json to config.js

## Foreign Key Setup

// Modify `associate()` function in models

Example:

**\*Ideas** had foreign key from **Users\***

Users Table

```
static associate(models) {
      // define association here
      Users.hasMany(models.Ideas, {
        foreignKey: "userid",
      });
    }
```

Ideas Table

```
static associate(models) {
      // define association here
      Ideas.belongsTo(models.Users, {
        foreignKey: "userid",
        onDelete: "CASCADE",
      });
    }
```

Migrations

Users Table

```
id: {
        allowNull: false,
        autoIncrement: true,
        primaryKey: true,
        type: Sequelize.INTEGER,
      },
      username: {
        type: Sequelize.STRING,
        allowNull: false,
        unique: true,
      },
```

Ideas Table

```
 userid: {
        type: Sequelize.INTEGER,
        onDelete: "CASCADE",
        references: {
          model: "Users",
          key: "id",
          as: "userid",
        },
      },
```
