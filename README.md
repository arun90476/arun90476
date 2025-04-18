Infra Requirements
Space Required: Approx. 150–200 MB

Java Version: Java SE 1.8

Server: Any server supporting Jetty/Java Servlet (Tomcat, Jetty, etc.)

Port Used: 8090 (can be configured)

2. Setup Steps
Install Java JDK 1.8+.

Place the utility package (attached or shared separately) on the server.

Navigate to the project root.

Use the following command to run:

bash
Copy code
java -jar target/jetty-webapp-1.0.0-SNAPSHOT-jar-with-dependencies.jar
The application will run on:

cpp
Copy code
http://<host>:8090
3. Utility Package
The utility package contains:

Backend Files: Java source code (.java files, pom.xml)

Frontend Files: HTML files under src/main/resources/webapp

Config: global.properties, logback.xml

Instructions: README with setup and execution guide

Let me know if any additional details are needed.

Best regards,
[Your Name]
