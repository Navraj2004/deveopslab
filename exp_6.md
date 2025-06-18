# Experiment 6: Gradle Build System

## Objective
To understand Gradle build tool, create a Gradle project, configure build scripts, manage dependencies, and execute various Gradle tasks for Java application development.

## Materials
- Java JDK 11 or higher
- Gradle build tool
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
```

### Step 2: Install Gradle
```bash
# Ubuntu/WSL - using package manager
sudo apt install gradle -y

# Verify installation
gradle --version
```

**Alternative: Download from Gradle website**
- Download from: `https://gradle.org/install/`
- Extract and add to system PATH

### Step 3: Initialize Gradle Project
```bash
# Create project directory
mkdir demo-project
cd demo-project

# Initialize Gradle project
gradle init
```

**Project Type Selection:**
- Select: **2** (application)
- Implementation language: **3** (Java)
- Build script DSL: **1** (Groovy)
- Test framework: **4** (JUnit Jupiter)
- Project name: **demo-project**
- Source package: **com.example**

### Step 4: Examine Project Structure
```
demo-project/
├── gradle/
│   └── wrapper/
├── gradlew            # Gradle wrapper (Unix)
├── gradlew.bat        # Gradle wrapper (Windows)
├── build.gradle       # Build configuration
├── settings.gradle    # Project settings
└── src/
    ├── main/
    │   └── java/
    │       └── com/
    │           └── example/
    │               └── App.java
    └── test/
        └── java/
            └── com/
                └── example/
                    └── AppTest.java
```

### Step 5: Examine Build Configuration

#### build.gradle
```gradle
plugins {
    id 'java'
    id 'application'
}

repositories {
    mavenCentral()
}

dependencies {
    testImplementation 'org.junit.jupiter:junit-jupiter:5.8.2'
}

java {
    sourceCompatibility = JavaVersion.VERSION_17
    targetCompatibility = JavaVersion.VERSION_17
}

application {
    mainClass = 'com.example.App'
}

tasks.named('test') {
    useJUnitPlatform()
}
```

#### settings.gradle
```gradle
rootProject.name = 'demo-project'
```

### Step 6: Examine Source Code

#### App.java
```java
package com.example;

public class App {
    public String getGreeting() {
        return "Hello World!";
    }

    public static void main(String[] args) {
        System.out.println(new App().getGreeting());
    }
}
```

### Step 7: Build the Project
```bash
# Clean and build project
gradle clean build
```

**Build Tasks Executed:**
- ✅ compileJava
- ✅ processResources  
- ✅ classes
- ✅ compileTestJava
- ✅ processTestResources
- ✅ testClasses
- ✅ test
- ✅ jar

### Step 8: Run the Application
```bash
# Execute the application
gradle run
```

**Expected Output:**
```
> Task :run
Hello World!
```

### Step 9: Execute Tests
```bash
# Run unit tests
gradle test
```

### Step 10: Generate JAR File
```bash
# Create distribution JAR
gradle jar

# JAR location: build/libs/demo-project.jar
```

### Step 11: Run JAR File
```bash
# Execute the generated JAR
java -cp build/libs/demo-project.jar com.example.App
```

## Common Gradle Tasks

| Task | Description | Command |
|------|-------------|---------|
| **build** | Complete build | `gradle build` |
| **clean** | Clean build directory | `gradle clean` |
| **compile** | Compile source code | `gradle compileJava` |
| **test** | Run tests | `gradle test` |
| **run** | Execute application | `gradle run` |
| **jar** | Create JAR file | `gradle jar` |
| **check** | Run all checks | `gradle check` |

## Advanced Gradle Commands

```bash
# List all available tasks
gradle tasks

# Build with info logging
gradle build --info

# Build without running tests
gradle build -x test

# Continuous build (watch for changes)
gradle build --continuous

# Generate project report
gradle projectReport

# Show dependency tree
gradle dependencies

# Refresh dependencies
gradle build --refresh-dependencies
```

## Gradle Wrapper Benefits
- **Version consistency**: Same Gradle version across environments
- **No installation required**: Downloads Gradle automatically
- **Cross-platform**: Works on Windows, Linux, macOS

### Using Gradle Wrapper
```bash
# Unix/Linux/macOS
./gradlew build
./gradlew run

# Windows
gradlew.bat build
gradlew.bat run
```

## Build Configuration Features

### Plugin Management
```gradle
plugins {
    id 'java'                    // Java compilation
    id 'application'             // Application plugin
    id 'jacoco'                  // Code coverage
    id 'checkstyle'             // Code style checking
}
```

### Dependency Management
```gradle
dependencies {
    // Compile-time dependencies
    implementation 'com.google.guava:guava:31.1-jre'
    
    // Test dependencies
    testImplementation 'org.junit.jupiter:junit-jupiter:5.8.2'
    testImplementation 'org.mockito:mockito-core:4.6.1'
    
    // Runtime dependencies
    runtimeOnly 'mysql:mysql-connector-java:8.0.29'
}
```

### Repository Configuration
```gradle
repositories {
    mavenCentral()              // Maven Central Repository
    gradlePluginPortal()        // Gradle Plugin Portal
    mavenLocal()                // Local Maven repository
    
    // Custom repository
    maven {
        url 'https://repo.example.com/maven'
    }
}
```

## Expected Results
- ✅ Gradle project initialized successfully
- ✅ Build completes without errors
- ✅ Tests pass successfully
- ✅ Application runs and displays "Hello World!"
- ✅ JAR file generated in build/libs directory

## Gradle vs Maven Comparison

| Feature | Gradle | Maven |
|---------|--------|-------|
| **Configuration** | build.gradle (DSL) | pom.xml (XML) |
| **Performance** | Faster (incremental builds) | Slower |
| **Flexibility** | High (programmable) | Limited |
| **Learning Curve** | Moderate | Easy |
| **Plugin Ecosystem** | Growing | Mature |

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Gradle command not found | Install Gradle or use wrapper |
| Build failures | Check build.gradle syntax |
| Java version conflicts | Set sourceCompatibility in build.gradle |
| Dependency resolution issues | Check repository configuration |

## Best Practices
1. **Use Gradle Wrapper**: Ensures version consistency
2. **Incremental Builds**: Leverage Gradle's build cache
3. **Modular Projects**: Organize large projects into modules
4. **Custom Tasks**: Create reusable build logic
5. **Build Scans**: Monitor build performance

## Conclusion
This experiment demonstrates Gradle build system capabilities, from project initialization to application execution. Gradle provides flexible, high-performance build automation with powerful dependency management, making it ideal for modern Java development and CI/CD integration.
