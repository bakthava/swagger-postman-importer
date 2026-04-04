# Swagger / Postman Importer for JMeter

A JMeter plugin (version **1.1**) that lets you instantly convert **OpenAPI/Swagger** specifications and **Postman collections** into fully-formed JMeter Test Plans (`.jmx`), saving hours of manual scripting.

---

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Benefits](#benefits)
- [Requirements](#requirements)
- [Installation](#installation)
- [Usage](#usage)
- [Building from Source](#building-from-source)
- [License](#license)

---

## Overview

`swagger-postman-importer` is a JMeter GUI plugin that adds an **"Import Swagger/Postman"** menu entry to the JMeter _Tools_ menu.  
Select a Swagger/OpenAPI (JSON or YAML) or Postman Collection (JSON) file, and the plugin parses it to produce a ready-to-run JMeter Test Plan containing HTTP Request samplers, Thread Groups, and per-request configuration – all without writing a single line of JMeter XML by hand.

---

## Features

| Feature | Details |
|---------|---------|
| **OpenAPI 2.0 (Swagger)** | Parses `swagger: "2.0"` JSON/YAML specifications |
| **OpenAPI 3.x** | Parses `openapi: "3.x.x"` JSON/YAML specifications |
| **Postman Collections v2 / v2.1** | Parses exported Postman Collection JSON files |
| **YAML support** | Transparently converts YAML input to JSON before parsing |
| **HTTP Methods** | Supports GET, POST, PUT, PATCH, DELETE, HEAD, OPTIONS |
| **Request bodies** | Captures JSON and form-data request bodies |
| **Path / query parameters** | Auto-populates parameter placeholders |
| **Automatic host & port detection** | Reads `host`, `basePath`, and `servers` entries |
| **Protocol detection** | Sets HTTP or HTTPS from the specification |
| **JMX output** | Produces a standards-compliant `.jmx` Test Plan file |
| **Non-destructive** | Does **not** modify the currently open Test Plan in memory |

---

## Benefits

- **Faster test creation** – Convert an entire API definition to a JMeter script in seconds.
- **Accuracy** – Eliminates copy-paste errors that occur during manual scripting.
- **API-first workflow** – Keep test scripts in sync with the API contract by re-importing whenever the specification changes.
- **Zero configuration** – Works out of the box; no extra JMeter properties or environment variables required.
- **JDK 8 compatible** – Runs on any JMeter 5.x installation backed by Java 8 or later.

---

## Requirements

| Component | Minimum Version |
|-----------|----------------|
| Apache JMeter | 5.6.3 |
| Java (JDK/JRE) | 8 |

---

## Installation

### Option A – Drop-in JAR (recommended)

1. Download `swagger-postman-importer-1.1.jar` from the [Releases](../../releases) page.
2. Copy the JAR into JMeter's plugin directory:
   ```
   $JMETER_HOME/lib/ext/swagger-postman-importer-1.1.jar
   ```
3. (Re)start JMeter.

### Option B – JMeter Plugins Manager

If you use the [JMeter Plugins Manager](https://jmeter-plugins.org/install/Install/):

1. Open **Options → Plugins Manager** in JMeter.
2. Search for **Swagger / Postman Importer**.
3. Click **Apply Changes and Restart JMeter**.

---

## Usage

1. Launch JMeter.
2. Open the **Tools** menu and click **Import Swagger / Postman**.
3. In the file-chooser dialog, select one of:
   - An **OpenAPI/Swagger** file (`.json` or `.yaml` / `.yml`)
   - A **Postman Collection** file (`.json`)
4. Choose the destination `.jmx` file when prompted.
5. Open the generated `.jmx` file via **File → Open** (or merge it into an existing plan).

> **Tip:** The generated Test Plan uses default Thread Group settings (1 user, 1 loop). Adjust ramp-up time and thread count before running a load test.

---

## Building from Source

```bash
# Prerequisites: JDK 8+, Apache Maven 3.6+
git clone https://github.com/bakthava/swagger-postman-importer.git
cd swagger-postman-importer
mvn clean package -DskipTests
# Output: target/swagger-postman-importer-1.1.jar
```

Copy the produced JAR to `$JMETER_HOME/lib/ext/` as described in [Installation](#installation).

---

## License

This project is licensed under the **Apache License 2.0** – see the [LICENSE](LICENSE) file for details.

