<properties>
    <jetty.version>12.0.5</jetty.version>
</properties>

<dependencies>
    <!-- Core Jetty EE10 -->
    <dependency>
        <groupId>org.eclipse.jetty.ee10</groupId>
        <artifactId>jetty-ee10</artifactId>
        <version>${jetty.version}</version>
    </dependency>
    
    <!-- Servlet Support -->
    <dependency>
        <groupId>org.eclipse.jetty.ee10</groupId>
        <artifactId>jetty-ee10-servlet</artifactId>
        <version>${jetty.version}</version>
    </dependency>
    
    <!-- WebApp Support -->
    <dependency>
        <groupId>org.eclipse.jetty.ee10</groupId>
        <artifactId>jetty-ee10-webapp</artifactId>
        <version>${jetty.version}</version>
    </dependency>
</dependencies>
