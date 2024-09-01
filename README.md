
# Periodic Table Database

This project is part of the FreeCodeCamp Relational Database certification. The objective is to build a database that stores information about the elements in the periodic table, along with a Bash script that interacts with this database to retrieve and display data in a user-friendly format.

## Project Structure

- **Database**: The database is created and managed using PostgreSQL.
- **Script**: A Bash script (`element.sh`) is provided to interact with the database.

### Files

- `periodic_table.sql`: Contains SQL commands to create the database, including the necessary tables and relations to store the elements, their properties, and types.
- `element.sh`: A Bash script to retrieve information from the database based on the user's input (either an element's name or atomic number).

## Database Schema

The database consists of the following tables:

1. **`elements`**:
   - `atomic_number`: The atomic number of the element (Primary Key).
   - `symbol`: The chemical symbol of the element.
   - `name`: The name of the element.

2. **`properties`**:
   - `atomic_number`: Foreign key referencing `elements`.
   - `atomic_mass`: The atomic mass of the element.
   - `melting_point_celsius`: The melting point of the element in Celsius.
   - `boiling_point_celsius`: The boiling point of the element in Celsius.

3. **`types`**:
   - `type_id`: Primary key for types of elements (e.g., metal, nonmetal).
   - `type`: The type of the element.

4. **`JOIN` tables**:
   - Relationships between `elements`, `properties`, and `types` are created using the `JOIN` SQL command.

## Usage

### Prerequisites

- PostgreSQL should be installed and running on your machine.
- The database should be created and populated using the provided `periodic_table.sql` file.

### Running the Script

The `element.sh` script can be run from the command line:

```bash
./element.sh <element_name_or_atomic_number>
```

- **Argument**: The script accepts either the name or atomic number of an element.
- **Output**: The script will return information about the element in a sentence format. For example:

```bash
The element with atomic number 1 is Hydrogen (H). It's a nonmetal, with a mass of 1.008 amu. Hydrogen has a melting point of -259.1 celsius and a boiling point of -252.9 celsius.
```

### Examples

```bash
./element.sh Hydrogen
```

```bash
./element.sh 1
```

### Error Handling

- If the element is not found, the script will output: `I could not find that element in the database.`
- If no argument is provided, the script will output: `Please provide an element as an argument.`

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

