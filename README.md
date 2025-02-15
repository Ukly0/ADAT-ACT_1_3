# Guía de Actividad 3: Proyecto Integrador – Miniaplicación de Acceso a Datos (Java)

Esta guía te ayudará a desarrollar una miniaplicación en **Java** que integre las funcionalidades de gestión de ficheros, manipulación de XML y conversión a otro formato (por ejemplo, JSON). Este proyecto está pensado para ser realizado en una sesión de 4 horas en aula.

---

## Tabla de Contenidos

- [Introducción](#introducción)
- [Objetivos](#objetivos)
- [Estructura del Proyecto](#estructura-del-proyecto)
- [Instalación y Requisitos](#instalación-y-requisitos)
- [Código de Ejemplo](#código-de-ejemplo)
  - [XmlConverter.java](#xmlconverterjava)
  - [Main.java](#mainjava)
  - [sample.xml](#samplexml)
- [Plan de Pruebas](#plan-de-pruebas)
- [Instrucciones de Uso](#instrucciones-de-uso)
- [Recursos y Documentación](#recursos-y-documentación)

---

## Introducción

En esta actividad, desarrollarás una miniaplicación en **Java** que:

- **Gestione ficheros:** Lee un archivo XML.
- **Manipule XML:** Extrae información del XML.
- **Convierta a otro formato:** Transforma el XML a JSON.
- **Incluya validación básica:** Maneje excepciones y realice comprobaciones de seguridad simples.

Esta aplicación permitirá aplicar y profundizar en los conceptos teóricos vistos en clase sobre la gestión de datos y seguridad en aplicaciones.

---

## Objetivos

- **Aplicar:** Programar clases que gestionen ficheros y manipulen XML.
- **Analizar:** Comparar y validar el proceso de conversión.
- **Evaluar y Crear:** Desarrollar e integrar la miniaplicación, documentando y justificando las decisiones técnicas.

---

## Estructura del Proyecto

La siguiente es una estructura básica recomendada para el proyecto:

```
miniapp-acceso-datos-java/
├── README.md                # Esta guía
├── pom.xml                  # Archivo Maven (si se usa Maven) o build.gradle para Gradle
├── .gitignore               # Archivos y carpetas a ignorar en Git
├── data/
│   └── sample.xml           # Archivo XML de ejemplo
├── src/
│   └── main/
│       └── java/
│           └── com/
│               └── ejemplo/
│                   ├── XmlConverter.java  # Clase para convertir XML a JSON
│                   └── Main.java          # Punto de entrada de la aplicación
└── test/
    └── java/
        └── com/
            └── ejemplo/
                └── XmlConverterTest.java # Pruebas unitarias para el conversor
```

---

## Instalación y Requisitos

- **Java 8 o superior**
- **Maven** o **Gradle** para la gestión del proyecto (opcional).
- Dependencias:
  - Una biblioteca para conversión de XML a JSON (por ejemplo, [org.json](https://github.com/stleary/JSON-java)).

Si usas Maven, puedes agregar en el `pom.xml` la dependencia:

```xml
<dependency>
    <groupId>org.json</groupId>
    <artifactId>json</artifactId>
    <version>20210307</version>
</dependency>
```

---

## Código de Ejemplo

### XmlConverter.java

```java
package com.ejemplo;

import java.io.File;
import java.io.IOException;
import java.nio.file.Files;
import org.json.JSONObject;
import org.json.XML;

public class XmlConverter {

    public static String convertXmlToJson(String xmlFilePath) {
        try {
            File xmlFile = new File(xmlFilePath);
            String xmlContent = new String(Files.readAllBytes(xmlFile.toPath()), "UTF-8");
            JSONObject jsonObj = XML.toJSONObject(xmlContent);
            return jsonObj.toString(4);
        } catch (IOException e) {
            System.err.println("Error al leer o convertir el archivo XML: " + e.getMessage());
            return null;
        }
    }
}
```

### Main.java

```java
package com.ejemplo;

public class Main {

    public static void main(String[] args) {
        String xmlFile = "data/sample.xml";
        String jsonResult = XmlConverter.convertXmlToJson(xmlFile);
        if (jsonResult != null) {
            System.out.println("Conversión exitosa. Resultado JSON:");
            System.out.println(jsonResult);
        } else {
            System.out.println("La conversión falló. Verifica el archivo XML.");
        }
    }
}
```

---

## Instrucciones de Uso

1. **Clona el repositorio**:
   ```bash
   git clone https://github.com/tuusuario/miniapp-acceso-datos-java.git
   cd miniapp-acceso-datos-java
   ```
2. **Compila el proyecto** (usando Maven, por ejemplo):
   ```bash
   mvn clean compile
   ```
3. **Ejecuta la aplicación**:
   ```bash
   mvn exec:java -Dexec.mainClass="com.ejemplo.Main"
   ```

---

## Recursos y Documentación

- [Documentación de org.json](https://github.com/stleary/JSON-java)
- [Tutorial de manejo de archivos en Java](https://docs.oracle.com/javase/tutorial/essential/io/)
- [Introducción a XML y JSON en Java](https://www.baeldung.com/java-xml-json)

---

> **Nota:**  
> Esta guía se ha elaborado en el contexto del IES Virgen del Carmen en Jaén, donde la demanda de profesionales en tecnologías de la información impulsa el aprendizaje práctico. La miniaplicación permite a los alumnos aplicar y consolidar conocimientos sobre la gestión de datos, seguridad en el acceso a datos y conversión de formatos, habilidades esenciales para su futura inserción en el mercado laboral.

