// Use ServletContext to load from WEB-INF
try (InputStream input = getServletContext().getResourceAsStream("/WEB-INF/global.properties")) {
    Properties props = new Properties();
    props.load(input);
    
    // Example: Get DB config
    String dbUrl = props.getProperty("db.url");
    response.getWriter().println("DB URL (Tomcat): " + dbUrl);
} catch (IOException e) {
    response.getWriter().println("Error loading properties: " + e.getMessage());
}
