# Database
## What is a database
- A database is a piece of software specialized in efficiently storing and retrieving data in a persistent manner (i.e. to disk).
- Databases are mainly divided in 2 big families: relational and non-relational.
## Relational databases
- In a relational database you need to define in advance the structure of your data, and the relationship between data entities.
- The standard language for relational databases is SQL, which means “structured query language”. Popular SQL implementations are the MySQL, PostgreSQL, and SQLite databases.
- Data is divided into tables, and each table is divided into columns and rows, where each column can store a pre-defined data type.
- A unique identifier for a row in a table can be used as a “primary key”.
- When a table includes a reference to the primary key of another table it’s called a “foreign key”.
- Tables can have relations between them. The main type of relations are:
  - One to one
  - One to many
  - Many to many
- if one to one relationship (user and driving licence) it is still good to use different tables - modularization, as creation of one is not dependent on another.
- search by PK would be logarithmic as the keys can be sorted. If not on PK would be linear as would have to go through each row. that is why we use indexes.
- Indexes are sorted versions of the respective columns (with the associated primary key for each entry), which allow to improve query time from linear to logarithmic.
- indexes also have tradeoffs - read speed increases but write speed is slow as we have to rewrite in both table and the btree of the index. also storage but that is minor
- Joins are a way to combine data from different tables, by using a matching condition. Each operation involves two tables: a “left” and a “right” one, which can be joined in four ways:
  - Inner - Returns only records that satisfy the matching condition in both tables.
  - Full outer - Returns all records from both tables, matched where possible.
  - Left / right - Contains all records from one table, but only the ones that satisfy the matching condition from the other.

## Sharding and replicating
- Sharding means dividing database data into several partial instances, typically to store them on different machines, as it wouldn’t otherwise fit all in one place.
- Replicating means writing the same data in multiple places, for safety purposes.
- Both sharding and replicating present their challenges in terms of data atomicity and integrity guarantees, while maintaining high performance in reads and writes.

[SQL cheat sheet](https://learnsql.com/blog/sql-basics-cheat-sheet/sql-basics-cheat-sheet-a4.pdf)
[tutorial](https://sqlbolt.com/)

## client
- just a piece of software that allows us to connect to the database

## ORM
- ORM means “object relational mapping”.
- ORM libraries allow to perform operations in a database, mapping them to “objects” that can be natively used in an object-oriented programming language.
- customize validation as well as migration functions
```javascript
// models/user.js
module.exports = (sequelize, DataTypes) => {
  const User = sequelize.define('User', {
    username: DataTypes.STRING
  });
  User.associate = db => {
    db.User.hasMany(db.Task);
  };
  return User;
};
```
```javascript
// models/task.js
module.exports = (sequelize, DataTypes) => {
  const Task = sequelize.define('Task', {
    title: DataTypes.STRING
  });
  Task.associate = db => {
    db.Task.belongsTo(db.User, {
      onDelete: "CASCADE",
      foreignKey: { allowNull: false }
    });
  };
  return Task;
};
```

```javascript
// models/index.js
const fs = require('fs');
const path = require('path');
const Sequelize = require('sequelize');

const config = {
  host: 'localhost',
  dialect: 'type'
};

const sequelize = new Sequelize('database', 'username', 'password', config);
const db = {};

const files = fs.readdirSync(__dirname);

for (const file of files) {
  if (file !== 'index.js') {
    const model = require(path.join(__dirname, file))(sequelize, Sequelize.DataTypes);
    db[model.name] = model;
  }
}

for (const model in db) {
  if (db[model].associate) db[model].associate(db);
}

db.sequelize = sequelize;
db.Sequelize = Sequelize;

module.exports = db;
```

```javascript
// index.js
const Koa = require('koa');
const app = new Koa();

const db = require('./models/index.js');
const router = require('./router.js');

app
  .use(router.routes())
  .use(router.allowedMethods());

(async function bootstrap () {
  await db.sequelize.sync();
  app.listen(3000);
})();
```
```javascript
// router.js
const Router = require('koa-router');

const usrController = require('./controllers/user.js');

const router = new Router();

router.get('/', usrController.getAll);

module.exports = router;
```
```javascript
// controllers/user.js
const fs = require('fs/promises');

const db  = require('../models/index.js');
const views = require('../views/index.js');

exports.getAll = async ctx => {
  const users = await db.User.findAll({ include: [ db.Task ] });
  ctx.body = views.home({ users });
};
```
```javascript
// views/index.js
const fs = require('fs');
const path = require('path');
const Handlebars = require('handlebars');

const views = {};

const files = fs.readdirSync(__dirname);

for (const file of files) {
  const ext = path.extname(file);
  const name = path.basename(file, ext);
  if (ext === '.html') {
    const content = fs.readFileSync(path.join(__dirname, file), 'utf8');
    views[name] = Handlebars.compile(content);
  }
}

module.exports = views;
```


## Non-relational databases
- Non-relational databases (aka “NoSQL”) don’t enforce any predefined structure on your data.
- The main families of non-relational databases are: document, key-value, and graph.
- They are more convenient to handle unstructured data or changing application requirements.
- On the other hand, your application logic can make less assumptions on the data available, and efficient queries need to be built ad-hoc.
- key-value - in RAM, very speed using key value pairs. Good for caching or session tokens
- graph - best to store data that can be represented by graph - neo4J
- relational - give you ACID - every transaction is either entirely executed or nothing at all
- non relational - write speed, flexible schema, horizontal scaling