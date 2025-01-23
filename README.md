# OpenTelemetry Java Agent with SigNoz Integration Documentation

## Overview

This documentation explains how to integrate OpenTelemetry Java agent with SigNoz for tracing and how to troubleshoot common issues, such as connection reset errors.

---

## Prerequisites

- **SigNoz Service**: Ensure that your SigNoz instance is running and accessible. This guide assumes SigNoz is self-hosted on an EC2 Linux server, which is commonly used for gRPC-based communication.
- **OpenTelemetry Java Agent**: You must have the OpenTelemetry Java agent JAR available for instrumenting your Java application.
- **Java 8 or Higher**: You must have Java 8 or higher installed on your instance.

---

## Step 1: Installation of Java 23 Debian Package

1. **Download the Package**  
   Navigate to the Oracle Java Downloads page and download the Debian package for JDK 23. Alternatively, use the following command to download it directly:

   ```bash
   wget <link-to-jdk23-debian-package>
   ```

2. **Install the Package**  
   After downloading, install the package using `apt`:

   ```bash
   sudo apt install ./<jdk23-package-name>.deb
   ```

3. **Verify the Installation**  
   Confirm the installation by checking the Java version:

   ```bash
   java -version
   ```

   You should see output similar to:

   ```plaintext
   java version "23.x.x"
   Java(TM) SE Runtime Environment (build 23.x.x)
   Java HotSpot(TM) 64-Bit Server VM (build x.x.x)
   ```

---

## Step 2: Setting up Sample Spring Boot Application

For this tutorial, we will use the popular **Spring PetClinic** application and integrate it with OpenTelemetry.

### About Spring PetClinic

The Spring PetClinic application is a well-known sample application used to demonstrate the capabilities of the Spring Framework in Java. It is a web application that uses Spring MVC (Model-View-Controller) to handle web requests, manage controllers, and render views. You can read more about it [here](https://github.com/spring-projects/spring-petclinic).

1. **Clone the Repository**

   ```bash
   git clone https://github.com/spring-projects/spring-petclinic.git
   cd spring-petclinic
   ```

2. **Run the Application**

   ```bash
   ./mvnw spring-boot:run
   ```

   If your application runs successfully, you will be able to access the application UI at:  
   [http://localhost:8090/](http://localhost:8090/)

---

## Step 3: Integration with Java Application

To instrument your Java application with OpenTelemetry, follow these steps:

1. **Download OpenTelemetry Java Agent**  
   Download the OpenTelemetry Java agent JAR from the [OpenTelemetry GitHub Releases](https://github.com/open-telemetry/opentelemetry-java-instrumentation/releases).

   > **Note:** Save the agent JAR in a folder named `java-agent` inside your project for better organization.

2. **Run Your Application with the OpenTelemetry Agent**

   ```bash
   java -javaagent:/path/to/opentelemetry-javaagent.jar -jar /path/to/your/application.jar
   ```

   Replace `/path/to/your/application.jar` with the actual path to your application’s JAR file.

   - To enable debug logging, add the following flag:
     ```bash
     -Dotel.javaagent.debug=true
     ```

---

## Step 4: Monitoring Your Spring Boot Application in SigNoz

1. **Generate Load**  
   Access the Spring PetClinic app at: [http://localhost:8090/](http://localhost:8090/) and play around with it to generate some load. For example, refresh endpoints multiple times.

2. **View in SigNoz Dashboard**  
   Open the **Services** tab of the SigNoz dashboard. You should see your Spring Boot application being monitored.

   - If you are a first-time user, follow the onboarding flow for Java applications to instrument your own Spring Boot application.

---

## Application Metrics and Traces

SigNoz makes it easy to visualize metrics and traces captured through OpenTelemetry instrumentation. Below are some examples:

- **Application Metrics and Logs**  
  Metrics and logs from the PetClinic Spring Boot application can help identify key operations.

- **Traces**  
  Traces for key operations in the application are captured and displayed for better monitoring and debugging.

---

## Troubleshooting

### 1. Check SigNoz Configuration
- Ensure the SigNoz instance is configured to receive traces over gRPC at port `4317`.
- Check for any proxy or firewall blocking the communication.
- Review SigNoz configuration files and logs for any errors.

### 2. OpenTelemetry Java Agent Version Compatibility
- Ensure the OpenTelemetry Java agent is compatible with your application and backend.
- If issues arise, consider upgrading or downgrading to a stable version.

### 3. Enable Debug Logging
- For detailed logs, enable debug logging:

  ```bash
  java -javaagent:/path/to/opentelemetry-javaagent.jar -Dotel.javaagent.debug=true -jar /path/to/your/application.jar
  ```

- Check the logs for additional information about connection issues.

---

## Additional Resources

- [OpenTelemetry Java Instrumentation Documentation](https://opentelemetry.io/docs/instrumentation/java/)
- [SigNoz Documentation](https://signoz.io/docs/)
- [OpenTelemetry GitHub Repository](https://github.com/open-telemetry/opentelemetry-java-instrumentation)

---

## Conclusion

By following the steps above, you should be able to set up OpenTelemetry with your Java application and troubleshoot any connectivity issues. If the problem persists, check the respective logs on the OpenTelemetry agent and SigNoz to gather more insights.
```

You can copy and save this content into a `.md` file, such as `README.md`, and add it to your GitHub repository. Let me know if you need further adjustments!
