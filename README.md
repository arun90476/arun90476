// ✅ Proper way to access WEB-INF in Tomcat
try (InputStream input = getServletContext()
        .getResourceAsStream("/WEB-INF/global.properties")) {
    
    if (input == null) {
        System.err.println("ERROR: File not found at: " + 
            getServletContext().getRealPath("/WEB-INF/global.properties"));
        return;
    }
    
    Properties props = new Properties();
    props.load(input);
    String value = props.getProperty("your.key");
    System.out.println("Value: " + value);

} catch (IOException e) {
    System.err.println("Failed to load properties: " + e.getMessage());
    e.printStackTrace();
}
