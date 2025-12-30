# Police Department Management System

A console-based C++ application for managing police department operations including officers, staff, criminals, cases, and witnesses.

## Table of Contents

- [Overview](#overview)
- [System Architecture](#system-architecture)
- [Features](#features)
- [Technical Specifications](#technical-specifications)
- [Installation and Setup](#installation-and-setup)
- [Usage](#usage)
- [Known Issues and Limitations](#known-issues-and-limitations)
- [Future Enhancements](#future-enhancements)
- [License](#license)

## Overview

This Police Department Management System is designed to streamline administrative operations within a police department. The system provides functionality to manage personnel records, criminal databases, case files, and witness information through a menu-driven console interface.

## System Architecture

### Class Hierarchy

The application follows an object-oriented design with the following core classes:

#### 1. `police_system` (Main Controller Class)
- Central management class coordinating all operations
- Contains vectors of officers, staff, criminals, cases, and witnesses
- Implements CRUD operations for all entities
- Manages data initialization and user interactions

#### 2. `officer`
- Encapsulates police officer information
- **Attributes**: ID, name, position, phone number, NID
- **Methods**: Display officer details, retrieve officer ID, update position

#### 3. `criminal`
- Manages criminal records
- **Attributes**: ID, name, cell number, crime description, punishment duration
- **Methods**: Display criminal details, retrieve ID and punishment duration
- Declared as friend class to `police_case` for integrated case management

#### 4. `staff`
- Handles non-officer personnel data
- **Attributes**: ID, name, position, phone number, NID
- **Methods**: Display staff details, retrieve ID and position

#### 5. `police_case`
- Manages case information and status tracking
- **Attributes**: Case ID, description, criminal name, case status
- **Methods**: Display case details, retrieve case ID
- Automatically creates criminal records for solved cases

#### 6. `witness`
- Stores witness testimonies
- **Attributes**: Name, age, statement
- **Methods**: Display witness information, retrieve age

### Design Patterns

- **Encapsulation**: All classes use private data members with public getter/setter methods
- **Friend Functions**: `promote_officer()` and `add_initial_data()` have privileged access to `police_system` internals
- **Vector-based Storage**: Dynamic arrays (STL vectors) for flexible data management

### Data Flow

```
User Input → Main Menu → police_system Methods → Individual Class Operations → Console Output
```

The system operates in a continuous loop until the user chooses to exit, with password authentication at startup.

## Features

### Core Functionalities

1. **Information Display**
   - View all officers, criminals, staff, cases, and witnesses
   - Formatted console output for each entity type

2. **Search Operations**
   - Search officers, staff, criminals, and cases by ID
   - Search witnesses by age
   - Real-time feedback on search results

3. **Data Entry**
   - Add multiple records in batch mode
   - Interactive prompts for all required fields
   - Automatic criminal record creation for solved cases

4. **Record Management**
   - Remove officers and staff by ID
   - Remove criminals with punishment duration validation
   - Legal compliance checks for criminal removal

5. **Officer Promotion**
   - Update officer positions
   - ID-based promotion system

6. **Security**
   - Password-protected access (default: "tutturu")
   - Masked password input using getch()

### Pre-loaded Data

The system includes sample data for demonstration:
- 3 officers (Commissioner, Deputy Commissioner, Officer-In-Charge)
- 3 criminals with various offenses
- 3 staff members (Food Observer, Floor Cleaner, Security Guard)
- 3 cases (SOLVED, UNSOLVED, ONGOING)

## Technical Specifications

### Development Environment

- **Language**: C++
- **Compiler**: Code::Blocks (project files included)
- **Standard Libraries**: 
  - `<bits/stdc++.h>` (GCC-specific aggregate header)
  - `<conio.h>` (Windows-specific console I/O)

### Dependencies

- GCC/G++ compiler with C++11 or higher
- Windows operating system (due to `conio.h` dependency)
- Code::Blocks IDE (optional, project files provided)

### Project Structure

```
Assignment of 2107004/
├── main.cpp                          # Main source code
├── Assignment of 2107004.cbp         # Code::Blocks project file
├── Assignment of 2107004.depend      # Dependency file
├── Assignment of 2107004.layout      # IDE layout configuration
├── bin/
│   └── Debug/                        # Debug executable output
└── obj/
    └── Debug/                        # Object files
```

## Installation and Setup

### Prerequisites

1. Install a C++ compiler (GCC/MinGW recommended for Windows)
2. Install Code::Blocks IDE or use command-line compilation

### Compilation Instructions

#### Using Code::Blocks
1. Open `Assignment of 2107004.cbp` in Code::Blocks
2. Select Build → Build (or press F9)
3. Run the executable from Build → Run

#### Using Command Line (Windows)
```bash
g++ main.cpp -o police_system.exe
police_system.exe
```

#### Using Command Line (Linux/Mac - requires modifications)
```bash
g++ main.cpp -o police_system -std=c++11
./police_system
```
Note: Linux/Mac compilation requires removing `conio.h` dependency and implementing alternative input methods.

## Usage

### Starting the Application

1. Run the compiled executable
2. Enter your name when prompted
3. Enter the password: `tutturu`
4. Navigate through the menu system using numeric options

### Menu Navigation

**Main Menu Options:**
1. Show Information - Display all records of selected entity type
2. Search Information - Find specific records by ID or age
3. Add Information - Create new records
4. Remove Information - Delete existing records
5. Promote Officer - Update officer positions
6. Quit - Exit the application

### Example Workflow

```
1. Select option 1 (Show Information)
2. Choose sub-option 1 (Show Police Information)
3. View all officer records
4. Press 'Y' to continue or 'N' to exit
```

## Known Issues and Limitations

### Critical Issues

1. **Non-Portable Headers**
   - `<bits/stdc++.h>` is GCC-specific and increases compilation time
   - `<conio.h>` limits platform compatibility to Windows
   - **Impact**: Cannot compile on Linux/Mac without modifications

2. **No Data Persistence**
   - All data stored in memory (STL vectors)
   - Data is lost when the application closes
   - **Impact**: Unsuitable for production use without database integration

3. **Security Vulnerabilities**
   - Password hardcoded in source code
   - No encryption or secure authentication
   - **Impact**: Unauthorized access risk

4. **Limited Input Validation**
   - Minimal error checking for user inputs
   - No validation for duplicate IDs
   - **Impact**: Potential for data corruption

### Design Issues

5. **Method Naming Inconsistency**
   - `get_officer_position()` actually sets the position (should be `set_officer_position()`)
   - Violates getter/setter naming conventions

6. **Namespace Pollution**
   - `using namespace std;` can cause naming conflicts
   - Not recommended for larger projects

7. **Random Number Generation**
   - Uses C-style `rand()` instead of modern `<random>` library
   - Seeded only once during case creation

8. **Criminal Removal Logic**
   - Requires manual entry of punishment duration for validation
   - Prone to user input errors

9. **Case-Criminal Relationship**
   - Solved cases automatically create criminal records
   - No bidirectional relationship maintenance
   - Duplicate criminal entries possible

10. **Search Limitations**
    - Witness search by age may return multiple results but only shows first match
    - No search by name or partial matching

### Minor Issues

11. **Magic Numbers**
    - Hardcoded values (e.g., password length = 7)
    - Cell numbers and punishment durations randomly generated without bounds checking

12. **Console Display**
    - No pagination for large datasets
    - Limited formatting options

## Future Enhancements

### High Priority

- **Database Integration**: Implement SQLite or MySQL for persistent storage
- **Cross-Platform Support**: Replace platform-specific headers with portable alternatives
- **Enhanced Security**: Implement proper authentication with encrypted password storage
- **Input Validation**: Add comprehensive validation for all user inputs

### Medium Priority

- **File I/O**: Enable data export/import (CSV, JSON)
- **Advanced Search**: Multi-criteria search with partial matching
- **Relationship Management**: Proper foreign key relationships between entities
- **Unit Testing**: Implement test suite for critical functions

### Low Priority

- **GUI Interface**: Develop graphical interface using Qt or similar framework
- **Reporting System**: Generate formatted reports and statistics
- **User Roles**: Implement role-based access control
- **Audit Logging**: Track all system operations with timestamps

## Contributing

This project is part of an academic assignment (Student ID: 2107004). Contributions, suggestions, and bug reports are welcome for educational purposes.

## License

This project is developed for educational purposes. Please ensure compliance with your institution's academic integrity policies before using or modifying this code.

---

**Project Type**: Console Application  
**Course**: Object-Oriented Programming (OOP)  
**Student ID**: 2107004  
**Development Period**: 2023-2024 Academic Year
