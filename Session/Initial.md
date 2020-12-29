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
