# Bash-DBMS

A lightweight Database Management System implemented entirely in Bash scripting. This project provides a command-line interface for creating databases, managing tables, and performing CRUD operations using simple file-based storage.

https://github.com/user-attachments/assets/94e2d6ca-995e-4803-b26f-2c43e9d104f7

## Table of Contents

- [🚀 Features](#-features)
  - [Database Management](#database-management)
  - [Table Management](#table-management)
  - [Data Operations](#data-operations)
  - [Data Types & Constraints](#data-types--constraints)
- [🏗️ Architecture](#️-architecture)
  - [Storage Structure](#storage-structure)
  - [File Format](#file-format)
- [📋 Prerequisites](#-prerequisites)
- [🛠️ Installation & Setup](#️-installation--setup)
- [📖 Usage Guide](#-usage-guide)
  - [Starting the DBMS](#starting-the-dbms)
  - [Database Operations](#database-operations)
    - [Create a Database](#create-a-database)
    - [Connect to Database](#connect-to-database)
  - [Table Operations](#table-operations)
    - [Create a Table](#create-a-table)
    - [Insert Data](#insert-data)
    - [Query Data](#query-data)
    - [Update Records](#update-records)
    - [Delete Records](#delete-records)
- [🔧 Technical Details](#-technical-details)
  - [Lock Mechanism](#lock-mechanism)
  - [Validation Rules](#validation-rules)
  - [Error Handling](#error-handling)
- [🎨 User Interface](#-user-interface)
  - [Color Coding](#color-coding)
  - [Interactive Menus](#interactive-menus)
- [🔒 Limitations](#-limitations)
- [🤝 Contributing](#-contributing)
  - [Development Guidelines](#development-guidelines)
- [📄 License](#-license)
- [🙏 Acknowledgments](#-acknowledgments)


## 🚀 Features

### Database Management
- **Create Databases**: Create new databases with validation
- **List Databases**: View all existing databases
- **Connect to Databases**: Interactive database connection
- **Drop Databases**: Remove databases with confirmation

### Table Management
- **Create Tables**: Define tables with multiple columns and data types
- **Delete Tables**: Remove tables from databases
- **Show Tables**: List all tables in a database
- **Add Columns**: Extend existing tables with new columns

### Data Operations
- **Insert Records**: Add new data with type validation and primary key constraints
- **Select Records**: Query data with filtering and comparison operators
- **Delete Records**: Remove specific records based on conditions
- **Update Records**: Modify existing data with validation

### Data Types & Constraints
- **INT**: Integer values with full comparison operators (=, !=, <, >, <=, >=)
- **STRING**: Text data with equality comparisons
- **BOOLEAN**: True/false values
- **Primary Keys**: Unique constraints (exactly one per table)
- **Data Validation**: Type checking and input sanitization

## 🏗️ Architecture

### Storage Structure
```
Bash-DBMS/
├── mydb/                          # Database directory
│   └── database_name/             # Individual database
│       ├── table_name             # Table data file (CSV-like)
│       └── .table_name.metadata   # Table schema
├── main                           # Entry point script
│   ├── createDB                   # Database creation
│   ├── listAllDB                  # Database listing
│   ├── connectToDB                # Database connection
│   │   └── databaseActions        # Table operations menu
│   │       ├── createTable        # Table creation with schema definition
│   │       ├── deleteTable        # Table removal
│   │       ├── showTables         # Table listing
│   │       ├── selectFromTable    # Data querying
│   │       ├── deleteFromTable    # Record deletion
│   │       ├── insertToTable      # Record insertion
│   │       ├── updateInTable      # Update interface
│   │       │   └── UpdateRecord   # Update logic
│   │       └── addTableColumn     # Column addition
│   └── dropDB                     # Database deletion
├── checkForRepeatedColumnName     # Column uniqueness check
├── getColumnIndex                 # Column position lookup
├── getRows                        # Row filtering
├── getType                        # Column type retrieval
├── inputValidator                 # Data type validation
├── pkCheck                        # Primary key validation
├── GetAllDbs                      # Database enumeration
└── .gitignore                     # Git ignore file
```

### File Format
- **Data Files**: Colon-separated values (`value1:value2:value3`)
- **Metadata Files**: Column definitions (`name:type:is_primary_key`)

## 📋 Prerequisites

- **Bash**: Unix/Linux shell environment
- **Standard Tools**: `awk`, `sed`, `grep`, `cut` (typically pre-installed)

## 🛠️ Installation & Setup

1. **Clone or Download** the project files
2. **Make Scripts Executable**:
   ```bash
   chmod +x *.sh  # or chmod +x main createDB connectToDB ...
   ```
3. **Run the Application**:
   ```bash
   ./main
   ```

## 📖 Usage Guide

### Starting the DBMS
```bash
./main
```

### Database Operations

#### Create a Database
1. Select "🛠️ Create a database"
2. Enter database name (4-12 letters, A-Z a-z only)
3. Database directory is created in `./mydb/`

#### Connect to Database
1. Select "🔗 Connect to a database"
2. Choose from available databases
3. Access table management menu

### Table Operations

#### Create a Table
1. Select "🧾 Create Table"
2. Enter table name (4-12 letters)
3. Specify number of columns (1-100)
4. For each column:
   - Enter column name (2-12 letters)
   - Choose data type (INT/BOOLEAN/STRING)
   - Set primary key (exactly one required)

#### Insert Data
1. Select "➕ Insert To Table"
2. Choose table from list
3. Enter values for each column
4. Primary key uniqueness is enforced

#### Query Data
1. Select "🔍 Select From Table"
2. Choose table to query
3. View full table or filter by column
4. Use comparison operators for INT columns

#### Update Records
1. Select "✏️ Update In Table"
2. Choose table and specify:
   - Column to filter by
   - Comparison operator and value
   - Column to update and new value

#### Delete Records
1. Select "❌ Delete From Table"
2. Choose table and column to filter
3. Select comparison operator and value
4. Confirm deletion of matching records

## 🔧 Technical Details

### Lock Mechanism
- Uses `/tmp/mydbms.lockdir` to prevent concurrent access
- Automatic cleanup on exit

### Validation Rules
- **Database Names**: 4-12 letters only
- **Table Names**: 4-12 letters only
- **Column Names**: 2-12 letters only, unique per table
- **Primary Keys**: Exactly one per table, INT or STRING types

### Error Handling
- Input validation with user-friendly messages
- File existence checks
- Type validation for data entry
- Primary key constraint enforcement


## 🎨 User Interface

### Color Coding
- 🔴 **Red**: Errors and critical messages
- 🟡 **Yellow**: Warnings and info messages
- 🔵 **Blue**: Menus and prompts
- 🟢 **Green**: Success confirmations
- 🟣 **Cyan**: Headers and borders

### Interactive Menus
- Numbered selections for easy navigation
- Input validation with retry prompts
- Animated text for better user experience
- Clear screen management for clean interface

## 🔒 Limitations

- **Single User**: Lock mechanism prevents concurrent access
- **File-Based**: No advanced database features (transactions, indexing)
- **Memory**: Limited by system RAM for large datasets
- **No Relations**: No foreign keys or joins
- **Basic Types**: Only INT, STRING, BOOLEAN supported

## 🤝 Contributing

1. **Fork** the repository
2. **Create** a feature branch
3. **Make** your changes
4. **Test** thoroughly
5. **Submit** a pull request

### Development Guidelines
- Maintain Bash scripting best practices
- Add comments for complex logic
- Test edge cases and error conditions
- Follow existing naming conventions
- Update documentation for new features

## 📄 License

This project is open source. Feel free to use, modify, and distribute.

## 🙏 Acknowledgments

- Built as an educational project to demonstrate shell scripting capabilities
- Inspired by traditional database concepts
- Uses standard Unix tools for portability

---

**Note**: This is a learning project demonstrating database concepts in Bash. For production use, consider full-featured database systems like MySQL, PostgreSQL, or SQLite.
