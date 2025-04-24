   ServletContext context = getServletContext(); // ← Inherited from HttpServlet
    InputStream input = context.getResourceAsStream("/WEB-INF/global.properties");
