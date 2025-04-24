import org.eclipse.jetty.ee10.webapp.WebAppContext;
import org.eclipse.jetty.server.Server;
import org.eclipse.jetty.util.resource.ResourceFactory;

public class JakartaCompatibilityTest {
    public static void main(String[] args) throws Exception {
        // 1. Initialize server on port 8080 (not 000)
        Server server = new Server(8080);
        
        // 2. Configure webapp context
        WebAppContext webapp = new WebAppContext();
        webapp.setContextPath("/");  // Fixed method name (was setContentPath)
        
        // 3. Set resource base correctly
        webapp.setBaseResource(ResourceFactory.of(webapp)
            .newResource("./src/main/webapp"));  // Fixed path syntax
        
        // 4. Configure class scanning
        webapp.setAttribute(
            "org.eclipse.jetty.server.webapp.ContainerIncludeJarPattern", 
            ".*\\.jar|.*/classes/.*"  // Fixed pattern syntax
        );
        
        // 5. Link handler and start
        server.setHandler(webapp);  // Fixed method name (was ketHandler)
        server.start();
        
        System.out.println("Server started at http://localhost:8080");
        System.out.println("Press Ctrl+C to stop");
        server.join();
    }
}
