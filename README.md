# Service Claim Reconciliation Automation

A simple Java-based automation system for reconciling service claims.

## Folder Structure

```
Service Claim Recon Automation/
├── src/
│   └── ServiceClaimReconciliation.java    # Single Java file with all classes
├── config/
│   └── application.properties             # Configuration settings
├── logs/                                  # Application log files (auto-created)
├── data/                                  # Input/Output data files
├── target/                                # Maven build output
├── pom.xml                                # Maven configuration
├── DATABASE_SETUP.sql                     # Database schema
└── README.md                              # This file
```

## Quick Start

### Prerequisites
- Java JDK 11 or higher
- Apache Maven 3.6 or higher
- MySQL Server 5.7 or higher (must be running)
- Microsoft SQL Server JDBC Driver (for Azure Synapse)
- (Optional) SAP Java Connector (JCo) 3.1.x SDK (Requires `sapjco3.jar` and `sapjco3.dll` if using JCo for SAP)

### Step 1: Start MySQL

Ensure MySQL server is running:
```bash
# Windows
net start MySQL80

# Linux/Mac
sudo systemctl start mysql
```

### Step 2: Set Up Database

Run the SQL script:
```bash
mysql -u root -p < DATABASE_SETUP.sql
```

Or manually create database:
```sql
CREATE DATABASE claim_recon;
```

### Step 3: Configure Database Connection

Edit `config/application.properties`:
```properties
db.host=localhost         # Your MySQL host
db.port=3306              # Your MySQL port
db.name=claim_recon       # Database name
db.user=root              # MySQL username
db.password=password      # MySQL password
```

### Step 4: Build the Project

```bash
mvn clean package
```

This creates: `target/service-claim-recon.jar`

### Step 5: Run the Application

```bash
java -jar target/service-claim-recon.jar
```

**That's it!** The application will:
- Load configuration
- Connect to MySQL
- Fetch pending claims
- Process and reconcile them
- Display results

## Java File Description

Single Java file: `ServiceClaimReconciliation.java` contains:
- **ServiceClaimReconciliation** - Main entry point
- **ClaimReconciliationEngine** - Core processing logic
- **Claim** - Data model
- **ConfigManager** - Configuration management
- **DatabaseManager** - Database operations

## Troubleshooting

### Error: "Maven not found"
- Download Maven from: https://maven.apache.org/download.cgi
- Add Maven to PATH environment variable
- Verify: `mvn -version`

### Error: "MySQL connection refused"
- Verify MySQL server is running
- Check db.host, db.port in application.properties
- Ensure database exists

### Error: "Build failed"
- Run: `mvn clean`
- Check internet connection for dependencies
- Verify Java 11+ is installed

## Features
- ✓ Single Java file with all classes
- ✓ Maven-based build system
- ✓ MySQL database integration
- ✓ Batch claim processing
- ✓ Configuration management
- ✓ Windows and Linux support
- ✓ Automatic dependency management
- ✓ Executable JAR creation

## Version
1.0.0 - Initial Release
