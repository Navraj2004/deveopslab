# Experiment 5: Maven Project Creation and Management

## Objective
To understand Apache Maven build tool, create a Maven project from scratch, configure dependencies, and execute various Maven lifecycle phases for Java application development.

## Materials
- Java JDK 11 or higher
- Apache Maven
- Text editor or IDE
- Terminal/Command Prompt

## Prerequisites
- Java JDK installed and configured
- JAVA_HOME environment variable set
- Basic understanding of Java programming
- Command line familiarity

## Procedure

### Step 1: Install Java JDK
```bash
# Ubuntu/WSL
sudo apt update
sudo apt install openjdk-11-jdk -y

# Verify installation
java -version
javac -version
```

### Step 2: Install Maven
```bash
# Ubuntu/WSL
sudo apt install maven -y

# Verify installation
mvn -version
```

**Alternative: Download from Apache Maven website**
- Download from: `https://maven.apache.org`
- Extract and add to system PATH

### Step 3: Create Maven Project
```bash
# Using Maven archetype
mvn archetype:generate \
  -DgroupId=com.example \
  -DartifactId=demo-project \
  -DarchetypeArtifactId=maven-archetype-quickstart \
  -DinteractiveMode=false
```

**Project Structure Created:**
```
demo-project/
├── pom.xml
├── src/
│   ├── main/
│   │   └── java/
│   │       └── com/
│   │           └── example/
│   │               └── App.java
│   └── test/
│       └── java/
│           └── com/
│               └── example/
│                   └── AppTest.java
└── target/
```

### Step 4: Navigate to Project Directory
```bash
cd demo-project
```

### Step 5: Examine Project Files

#### pom.xml Configuration
```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
         http://maven.apache.org/xsd/maven-4.0.0.xsd">
    
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>demo-project</artifactId>
    <version>1.0-SNAPSHOT</version>
    <packaging>jar</packaging>
    
    <properties>
        <maven.compiler.source>11</maven.compiler.source>
        <maven.compiler.target>11</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>
    
    <dependencies>
        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter</artifactId>
            <version>5.8.2</version>
            <scope>test</scope>
        </dependency>
    </dependencies>
    
</project>
```

#### App.java Source Code
```java
package com.example;

public class App {
    public static void main(String[] args) {
        System.out.println("Hello, Maven Project Works!");
    }
}
```

### Step 6: Compile the Project
```bash
# Compile source code
mvn compile
```

**Expected Output:**
```
[INFO] Compiling 1 source file to /path/to/demo-project/target/classes
[INFO] BUILD SUCCESS
```

### Step 7: Run Tests
```bash
# Execute unit tests
mvn test
```

### Step 8: Package the Project
```bash
# Create JAR file
mvn package
```

**Generated Files:**
- `target/demo-project-1.0-SNAPSHOT.jar`
- `target/classes/` (compiled classes)

### Step 9: Run the JAR File
```bash
# Execute the packaged application
java -cp target/demo-project-1.0-SNAPSHOT.jar com.example.App
```

**Expected Output:**
```
Hello, Maven Project Works!
```

### Step 10: Clean the Project
```bash
# Remove target directory
mvn clean
```

## Maven Lifecycle Phases

| Phase | Description | Command |
|-------|-------------|---------|
| **validate** | Validate project structure | `mvn validate` |
| **compile** | Compile source code | `mvn compile` |
| **test** | Run unit tests | `mvn test` |
| **package** | Create JAR/WAR file | `mvn package` |
| **verify** | Run integration tests | `mvn verify` |
| **install** | Install to local repository | `mvn install` |
| **deploy** | Deploy to remote repository | `mvn deploy` |

## Common Maven Commands

```bash
# Full build lifecycle
mvn clean install

# Skip tests during build
mvn install -DskipTests

# Run specific test
mvn test -Dtest=AppTest

# Generate project documentation
mvn site

# Display dependency tree
mvn dependency:tree

# Check for dependency updates
mvn versions:display-dependency-updates
```

## Project Configuration Elements

### POM.xml Key Sections
- **groupId**: Organization identifier
- **artifactId**: Project name
- **version**: Project version
- **packaging**: Output format (jar, war, pom)
- **dependencies**: External libraries
- **properties**: Configuration variables
- **build**: Build configuration

### Directory Structure Convention
- `src/main/java`: Source code
- `src/main/resources`: Resources files
- `src/test/java`: Test source code
- `src/test/resources`: Test resources
- `target/`: Build output directory

## Expected Results
- ✅ Maven project created successfully
- ✅ Code compiles without errors
- ✅ Tests pass successfully
- ✅ JAR file generated in target directory
- ✅ Application runs and displays expected output

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Maven command not found | Install Maven and add to PATH |
| Compilation errors | Check Java version and JAVA_HOME |
| Test failures | Review test code and dependencies |
| Build failures | Verify pom.xml syntax |

## Advanced Features
- **Profiles**: Environment-specific configurations
- **Plugins**: Extended functionality
- **Multi-module projects**: Large project organization
- **Repository management**: Dependency distribution

## Conclusion
This experiment demonstrates Maven project lifecycle management, from creation to packaging. Maven provides standardized project structure, dependency management, and build automation, making it essential for Java development and CI/CD pipelines.
