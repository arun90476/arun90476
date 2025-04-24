import org.eclipse.jetty.ee10.webapp.WebAppContext;
import org.eclipse.jetty.server.Server;
import org.eclipse.jetty.util.resource.ResourceFactory;

public class JakartaCompatibilityTest {
    public static void main(String[] args) throws Exception {
        Server server = new Server(8080);
        
        // Initialize with Resource (recommended)
        WebAppContext webapp = new WebAppContext();
        webapp.setContextPath("/");
        webapp.setBaseResource(ResourceFactory.root()
            .newResource("./src/main/webapp"));
        
        server.setHandler(webapp);
        server.start();
        System.out.println("Server started: http://localhost:8080");
        server.join();
    }
}
