# Rails Migration Tutorial

## What is Rails Migration?

Rails Migration is a feature of Ruby on Rails that allows developers to manage and modify a database schema in a structured and version-controlled way. Instead of manually writing SQL statements to alter the database, migrations provide a Ruby DSL (Domain-Specific Language) to define changes.

Migrations enable:
- Database schema versioning
- Easy collaboration in teams
- Database independence (works across different databases like PostgreSQL, MySQL, SQLite, etc.)

Migrations are stored in the `db/migrate` directory, and each migration file is timestamped to track the order of execution.

## What Can Rails Migration Do?

Rails migrations can perform several operations on the database, including:

### 1. **Create and Drop Tables**
   - Creating a new table:
     ```ruby
     class CreateUsers < ActiveRecord::Migration[6.1]
       def change
         create_table :users do |t|
           t.string :name
           t.string :email
           t.timestamps
         end
       end
     end
     ```
   - Dropping a table:
     ```ruby
     class DropUsers < ActiveRecord::Migration[6.1]
       def change
         drop_table :users
       end
     end
     ```

### 2. **Add, Remove, Rename Columns**
   - Adding a column:
     ```ruby
     class AddAgeToUsers < ActiveRecord::Migration[6.1]
       def change
         add_column :users, :age, :integer
       end
     end
     ```
   - Removing a column:
     ```ruby
     class RemoveAgeFromUsers < ActiveRecord::Migration[6.1]
       def change
         remove_column :users, :age
       end
     end
     ```
   - Renaming a column:
     ```ruby
     class RenameEmailToContactEmail < ActiveRecord::Migration[6.1]
       def change
         rename_column :users, :email, :contact_email
       end
     end
     ```

### 3. **Change Column Type**
   ```ruby
   class ChangeAgeToString < ActiveRecord::Migration[6.1]
     def change
       change_column :users, :age, :string
     end
   end
   ```

### 4. **Add and Remove Indexes**
   - Adding an index:
     ```ruby
     class AddIndexToUsersEmail < ActiveRecord::Migration[6.1]
       def change
         add_index :users, :email, unique: true
       end
     end
     ```
   - Removing an index:
     ```ruby
     class RemoveIndexFromUsersEmail < ActiveRecord::Migration[6.1]
       def change
         remove_index :users, :email
       end
     end
     ```

### 5. **Add and Remove Foreign Keys**
   - Adding a foreign key:
     ```ruby
     class AddForeignKeyToPosts < ActiveRecord::Migration[6.1]
       def change
         add_foreign_key :posts, :users
       end
     end
     ```
   - Removing a foreign key:
     ```ruby
     class RemoveForeignKeyFromPosts < ActiveRecord::Migration[6.1]
       def change
         remove_foreign_key :posts, :users
       end
     end
     ```

## Running Migrations

### **1. Creating a Migration**
Generate a migration using:
```sh
rails generate migration MigrationName
```

For example, to add an `age` column to the `users` table:
```sh
rails generate migration AddAgeToUsers age:integer
```

### **2. Running Migrations**
Apply all pending migrations:
```sh
rails db:migrate
```

### **3. Rolling Back Migrations**
Undo the last migration:
```sh
rails db:rollback
```
Rollback a specific number of migrations:
```sh
rails db:rollback STEP=2
```

### **4. Checking Migration Status**
View applied and pending migrations:
```sh
rails db:migrate:status
```

## Conclusion
Rails Migrations simplify database schema management by allowing structured, version-controlled modifications. They help maintain consistency across different environments and ensure database changes are easily reversible.

By using migrations effectively, you can manage your database changes efficiently without manually writing SQL queries.

