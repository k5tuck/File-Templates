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
