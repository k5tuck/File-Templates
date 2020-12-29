## First Steps

Create Directory

```sh
mkdir app_name
cd app_name
```

Initialize NPM and Git

```sh
git init
npm -y init
```

Create Main `.js` file

```sh
touch index.js
```

## NPM Dependencies

```
npm i express express-es6-template-engine morgan helmet dotenv sequelize pg pg-hstore express-session session-file-store bcryptjs
```

```
npm i --save-dev nodemon sequelize-cli
```

Insert into index.js (Main) to parse Data from POST requests

```JavaScript
app.use(express.urlencoded({extended: true}));
```

## Create Gitignore File

Create File

```sh
touch .gitignore
```

Insert below into .gitignore

```
node_modules
config
sessions
.env
```
