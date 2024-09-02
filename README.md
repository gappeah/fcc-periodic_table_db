# Periodic Table Database

This project is part of the FreeCodeCamp Relational Database certification. The objective was to build a database that stores information about the elements in the periodic table and create a Bash script that interacts with this database to retrieve and display data in a user-friendly format.

## Project Structure

- **Database**: The database is managed using PostgreSQL.
- **Script**: A Bash script (`element.sh`) was created to interact with the database.

### Files

- `periodic_table.sql`: Contains SQL commands to create the database, including the necessary tables and relationships to store the elements, their properties, and types.
- `element.sh`: A Bash script to retrieve information from the database based on user input (either an element's name, symbol, or atomic number).

## Database Schema

The database consists of the following tables:
![diagram-export-02-09-2024-14_30_54](https://github.com/user-attachments/assets/748dca59-8ced-47b3-992a-89074b2fb8e5)


### `elements` Table

| Column Name    | Data Type | Constraints      |
| -------------- | --------- | ---------------- |
| `atomic_number`| INTEGER   | PRIMARY KEY      |
| `symbol`       | VARCHAR   | UNIQUE, NOT NULL |
| `name`         | VARCHAR   | UNIQUE, NOT NULL |

### `properties` Table

| Column Name            | Data Type | Constraints                            |
| ---------------------- | --------- | -------------------------------------- |
| `atomic_number`        | INTEGER   | REFERENCES `elements(atomic_number)`   |
| `atomic_mass`          | DECIMAL   | NOT NULL                               |
| `melting_point_celsius`| DECIMAL   | NOT NULL                               |
| `boiling_point_celsius`| DECIMAL   | NOT NULL                               |
| `type_id`              | INTEGER   | REFERENCES `types(type_id)`, NOT NULL  |

### `types` Table

| Column Name | Data Type | Constraints  |
| ----------- | --------- | ------------ |
| `type_id`   | INTEGER   | PRIMARY KEY  |
| `type`      | VARCHAR   | NOT NULL     |

## Usage

### Prerequisites

- **PostgreSQL**: Ensure PostgreSQL is installed and running on your machine. Connect to the database using:

  ```bash
  psql --username=freecodecamp --dbname=periodic_table
  ```

- **Database Setup**: The database should be created and populated using the provided `periodic_table.sql` file.

### Running the Script

The `element.sh` script can be run from the command line:

```bash
./element.sh <element_name_or_atomic_number>
```

- **Argument**: The script accepts either the name, symbol, or atomic number of an element.
- **Output**: The script returns detailed information about the element in a formatted sentence. For example:

  ```bash
  The element with atomic number 1 is Hydrogen (H). It's a nonmetal, with a mass of 1.008 amu. Hydrogen has a melting point of -259.1 celsius and a boiling point of -252.9 celsius.
  ```

### Error Handling

- If the element is not found, the script will output: `I could not find that element in the database.`
- If no argument is provided, the script will output: `Please provide an element as an argument.`

## Project Completion

### Fixing the Database

The database initially had a few issues that were resolved:

1. The `weight` column was renamed to `atomic_mass`.
2. The `melting_point` and `boiling_point` columns were renamed to `melting_point_celsius` and `boiling_point_celsius`, respectively.
3. The `melting_point_celsius` and `boiling_point_celsius` columns were updated to not accept null values.
4. The `UNIQUE` constraint was added to the `symbol` and `name` columns in the `elements` table.
5. The `atomic_number` column in the `properties` table was set as a foreign key referencing the `atomic_number` column in the `elements` table.
6. A `types` table was created to store the types of elements and was linked to the `properties` table.

### Git Repository

The project folder was initialized as a Git repository:

```bash
git init
```

The repository was ensured to have a `main` branch with at least five commits, using conventional prefixes like `fix:`, `feat:`, `refactor:`, etc.

### Bash Script

The `element.sh` script was developed to query and display information from the database. Example command:

```bash
./element.sh Hydrogen
```

Expected output:

```bash
The element with atomic number 1 is Hydrogen (H). It's a nonmetal, with a mass of 1.008 amu. Hydrogen has a melting point of -259.1 celsius and a boiling point of -252.9 celsius.
```

### Notes

- To back up the database:

  ```bash
  pg_dump -cC --inserts -U freecodecamp periodic_table > periodic_table.sql
  ```

- To restore the database:

  ```bash
  psql -U postgres < periodic_table.sql
  ```

## Installation

1. Clone this repository.
2. Set up the database:
   - Log in to PostgreSQL:
     ```bash
     psql --username=freecodecamp --dbname=postgres
     ```
   - Run the SQL commands in `periodic_table.sql` to create and populate the database:
     ```sql
     \i periodic_table.sql
     ```
3. Make sure the `element.sh` script has execution permissions:
   ```bash
   chmod +x element.sh
   ```

4. Run the script as described above.
