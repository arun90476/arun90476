import org.eclipse.jetty.ee10.webapp.WebAppContext;
import org.eclipse.jetty.server.Server;
import org.eclipse.jetty.util.resource.ResourceFactory;

public class JakartaCompatibilityTest {
    public static void main(String[] args) throws Exception {
        Server server = new Server(8080);
        
        // Configure your webapp
        WebAppContext webapp = new WebAppContext();
        webapp.setContextPath("/");
        webapp.setBaseResource(ResourceFactory.of(webapp).newResource("./src/main/webapp"));
        webapp.setAttribute("org.eclipse.jetty.server.webapp.ContainerIncludeJarPattern", ".*\\.jar|.*/classes/.*");
        
        server.setHandler(webapp);
        server.start();
        
        System.out.println("Server started at http://localhost:8080");
        System.out.println("Press Ctrl+C to stop");
        server.join();
    }
}
