# Swagger / Postman Importer for JMeter

A powerful JMeter plugin that enables seamless import of Swagger/OpenAPI specifications and Postman collections to automatically generate JMeter test plans (.jmx files).

## 📋 Table of Contents
- [Features](#features)
- [Requirements](#requirements)
- [Installation](#installation)
- [Usage](#usage)
- [Supported Formats](#supported-formats)
- [Example](#example)
- [Troubleshooting](#troubleshooting)
- [Support](#support)

---

## ✨ Features

- **Swagger/OpenAPI Import** - Import API specifications in JSON and YAML formats
- **Postman Collection Import** - Convert Postman collections to JMeter test plans
- **Automatic Test Plan Generation** - Generate complete JMeter test plans (.jmx)
- **HTTP Sampler Creation** - Automatic HTTP sampler configuration from API definitions
- **Request Parameterization** - Extract and configure parameters from API specs
- **Menu Integration** - Seamless integration via JMeter Tools menu
- **Zero Runtime Overhead** - Plugin-on-demand loading

---

## 🖥️ Requirements

### System Requirements
| Requirement | Version |
|------------|---------|
| **JMeter** | 5.1.1 or higher |
| **Java JDK** | 1.8+ (Java 8, 9, 10, 11, 12, ..., 21) |
| **OS** | Windows, Linux, macOS |
| **Memory** | Minimum 512MB (1GB recommended) |

### Supported JDK Versions
- ✅ **Java 1.8 (LTS)** - Recommended for maximum compatibility
- ✅ **Java 11 (LTS)** - Recommended for modern environments
- ✅ **Java 17 (LTS)** - Fully supported
- ✅ **Java 21 (LTS)** - Fully supported
- ✅ **Java 9, 10, 12-16, 18-20** - Supported but not LTS

### Supported Formats
| Format | Version | Support |
|--------|---------|---------|
| **Swagger** | 2.0 (OpenAPI 2.0) | ✅ Full |
| **OpenAPI** | 3.0.x, 3.1.x | ✅ Full |
| **Postman** | v2.1 | ✅ Full |
| **JSON** | Any valid JSON | ✅ Supported |
| **YAML** | Any valid YAML | ✅ Supported |

---

## 📦 Installation

### Step 1: Download the Plugin JAR
Download the latest version of `swagger-postman-importer-1.1.jar`:

```bash
# From GitHub Release
wget https://github.com/bakthava/swagger-postman-importer/releases/download/v1.1/swagger-postman-importer-1.1.jar
```

**Or download directly from:** https://github.com/bakthava/swagger-postman-importer/releases

### Step 2: Locate JMeter Extensions Directory
Find your JMeter installation directory:

```bash
# Linux/macOS
$JMETER_HOME/lib/ext/

# Windows
C:\Program Files\apache-jmeter-x.x\lib\ext\
```

### Step 3: Copy JAR File
Place the downloaded JAR in the `lib/ext` directory:

```bash
# Linux/macOS
cp swagger-postman-importer-1.1.jar $JMETER_HOME/lib/ext/

# Windows - Using PowerShell
Copy-Item -Path "swagger-postman-importer-1.1.jar" -Destination "$env:JMETER_HOME\lib\ext\"
```

### Step 4: Restart JMeter
Completely restart JMeter for the plugin to load:

```bash
# Linux/macOS
$JMETER_HOME/bin/jmeter.sh

# Windows
%JMETER_HOME%\bin\jmeter.bat
```

### Step 5: Verify Installation
In JMeter:
1. Go to **Tools** menu
2. You should see **Swagger / Postman Importer** option
3. Click to open the importer dialog

✅ **Installation successful!**

---

## 🚀 Usage

### Basic Usage

#### 1. Open the Importer
- Go to **Tools** → **Swagger / Postman Importer**

#### 2. Select File Type
- Choose between:
  - **Swagger/OpenAPI** (.json or .yaml)
  - **Postman Collection** (.json)

#### 3. Select File
- Browse and select your API specification or Postman collection file

#### 4. Configure Options (Optional)
- **Base URL** - Override the base URL from the specification
- **Thread Group** - Set number of threads/users
- **Loop Count** - Set number of iterations
- **Ramp-up Time** - Configure ramp-up period

#### 5. Generate Test Plan
- Click **Import** or **Generate**
- The plugin creates a complete JMeter test plan (.jmx)

#### 6. Save Test Plan
- Save the generated test plan:
  - **File** → **Save As**
  - Choose location and give it a name
  - Extension will be `.jmx`

---

## 📋 Supported Formats

### Swagger / OpenAPI

**Example Swagger 2.0 Structure:**
```json
{
  "swagger": "2.0",
  "info": {
    "title": "Pet Store API",
    "version": "1.0.0"
  },
  "host": "petstore.swagger.io",
  "basePath": "/v1",
  "schemes": ["http"],
  "paths": {
    "/pets": {
      "get": {
        "operationId": "listPets",
        "parameters": [...],
        "responses": {...}
      }
    }
  }
}
```

### Postman Collection

**Example Postman v2.1 Structure:**
```json
{
  "info": {
    "name": "Pet Store API",
    "schema": "https://schema.getpostman.com/json/collection/v2.1.0/collection.json"
  },
  "item": [
    {
      "name": "Get Pets",
      "request": {
        "method": "GET",
        "url": "http://petstore.swagger.io/v1/pets"
      }
    }
  ]
}
```

---

## 💡 Example

### Scenario: Import Swagger Pet Store API

**Input:** `petstore-swagger.json` (Swagger 2.0 specification)

**Steps:**
1. Tools → Swagger / Postman Importer
2. Select "Swagger/OpenAPI"
3. Choose `petstore-swagger.json`
4. Set Thread Group = 5 users
5. Set Loop Count = 10
6. Click Generate
7. Save as `petstore-testplan.jmx`

**Output:** Complete JMeter test plan with:
- ✅ HTTP Request Samplers for all API endpoints
- ✅ Request headers and parameters
- ✅ Response assertions
- ✅ Configured Thread Group
- ✅ Listeners and aggregators

---

## 🔧 Advanced Configuration

### Command Line Usage
For headless/CLI usage with JMeter:

```bash
jmeter -n -t generated-testplan.jmx -l results.jtl -j jmeter.log
```

### Configuration File
Place configuration in `jmeter.properties`:

```properties
# Plugin-specific settings
swagger.postman.importer.timeout=30000
swagger.postman.importer.connect.timeout=10000
swagger.postman.importer.read.timeout=20000
```

---

## 🐛 Troubleshooting

### Plugin Not Showing in Tools Menu

**Problem:** "Swagger / Postman Importer" option missing from Tools menu

**Solutions:**
1. Verify JAR is in `$JMETER_HOME/lib/ext/` directory
2. Restart JMeter (fully close and reopen)
3. Check JMeter logs for errors:
   - Linux/macOS: `$JMETER_HOME/bin/jmeter.log`
   - Windows: `%JMETER_HOME%\bin\jmeter.log`
4. Verify correct JDK version (1.8+)

### Import Fails - Invalid Format

**Problem:** "File format not recognized" error

**Solutions:**
1. Verify file is valid JSON/YAML:
   ```bash
   # Validate JSON
   jq . petstore.json
   ```
2. Ensure correct file type selection in dialog
3. Check file encoding (UTF-8 recommended)
4. Download latest Swagger/Postman schema

### Memory Issues

**Problem:** OutOfMemoryError during large API import

**Solutions:**
1. Increase JMeter heap memory:
   ```bash
   # Linux/macOS
   export HEAP="-Xmx1g -Xms1g"
   
   # Windows - Edit jmeter.bat
   set HEAP=-Xmx1g -Xms1g
   ```
2. Split large collections into smaller files
3. Import in separate sessions

### JAR Conflicts

**Problem:** "Class not found" or duplicate class errors

**Solutions:**
1. Verify no conflicting plugins in `lib/ext/`
2. Remove duplicate JAR files
3. Check shading in JAR (should be under `com.example.shaded.org.json`)
4. Use only compatible JMeter version (5.1.1+)

---

## 📊 System Information

### Build Details
- **Version:** 1.1
- **Java Compiler:** Maven Compiler Plugin 3.11.0
- **Target Java:** 1.8 (JDK 8 compatible)
- **Maven Version:** 3.8.1+
- **Build Tool:** Maven with Shade Plugin

### Dependencies (Shaded)
- `org.json:json:20231013` (relocated to prevent conflicts)

### File Size
- Plugin JAR: ~100KB (with shaded dependencies)
- Minimal overhead on JMeter startup

---

## 📝 Version History

### v1.1 (Latest)
- ✅ Updated JMeter core dependencies to 5.6.3
- ✅ Upgraded JSON library to 20231013
- ✅ Optimized for Java 1.8+ compatibility
- ✅ Improved JAR shading for conflict prevention
- ✅ Removed unused dependencies (snakeyaml, JUnit)
- ✅ Better error messages and logging

### v1.0
- ✅ Initial release
- ✅ Support for Swagger/OpenAPI import
- ✅ Support for Postman collection import
- ✅ Automatic HTTP sampler generation

---

## 🤝 Support & Contribution

### Getting Help
- **GitHub Issues:** https://github.com/bakthava/swagger-postman-importer/issues
- **Discussion:** https://github.com/bakthava/swagger-postman-importer/discussions
- **Plugin Registry:** https://jmeter-plugins.org/

### Contributing
Contributions are welcome! Please:
1. Fork the repository
2. Create a feature branch
3. Submit a pull request with detailed description

### License
Apache License 2.0 - See LICENSE file for details

---

## 📚 Resources

- **JMeter Documentation:** https://jmeter.apache.org/
- **Swagger/OpenAPI Specification:** https://swagger.io/specification/
- **Postman Documentation:** https://learning.postman.com/
- **JMeter Plugins:** https://jmeter-plugins.org/
- **GitHub Repository:** https://github.com/bakthava/swagger-postman-importer

---

## ❓ FAQ

**Q: Does the plugin support both JSON and YAML formats?**  
A: Yes! Both Swagger 2.0 (JSON/YAML) and OpenAPI 3.0+ (JSON/YAML) are fully supported.

**Q: Can I use this plugin with JMeter 5.0?**  
A: The plugin requires JMeter 5.1.1 or higher. Please upgrade your JMeter installation.

**Q: What Java version do I need?**  
A: Java 1.8 (JDK 8) or higher. Java 8, 11, 17, and 21 LTS versions are officially supported.

**Q: Can I bulk import multiple Postman collections?**  
A: Currently, the plugin imports one collection per session. For multiple collections, run the importer multiple times or use scripting.

**Q: Is there command-line support?**  
A: The GUI is the primary interface. For automation, generate test plans via GUI and use `jmeter -n` command line mode.

**Q: How do I report a bug?**  
A: Visit https://github.com/bakthava/swagger-postman-importer/issues and create a new issue with details and error logs.

---

## 📧 Contact

For questions, suggestions, or feedback:
- **Author:** Bakthavachalam
- **Email:** via GitHub profile
- **GitHub:** https://github.com/bakthava

---

**Last Updated:** April 6, 2026  
**Version:** 1.1
