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
