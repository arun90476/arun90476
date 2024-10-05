<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Combined Page</title>
    <style>
        body {
            display: flex;
            flex-direction: column;
            margin: 0;
            font-family: Arial, sans-serif;
        }
        header {
           height: 55px;
            background-color: #343a40; /* Dark header background */
            color: white; /* White text */
            padding: 10px;
            text-align: center;
        }
        main {
            display: flex;
            flex-grow: 1;
        }
        #sidebar {
            width: 200px;
            background-color: teal; /* Sidebar background color */
            color: white; /* Text color */
            padding: 10px;
            box-shadow: 2px 0 5px rgba(0, 0, 0, 0.1);
        }
        #sidebar h3 {
            margin-top: 0;
        }
        #content {
            flex-grow: 1;
            padding: 10px;
            background-color: #f8f9fa; /* Content background color */
        }
        a {
            display: block;
            margin: 5px 0;
            text-decoration: none;
            color: white; /* Link color */
            transition: background-color 0.3s;
            padding: 8px;
            border-radius: 4px; /* Rounded corners */
        }
        a:hover {
            background-color: #0056b3; /* Darker blue on hover */
        }
        footer {
            height: 40px;
            background-color: #343a40; /* Dark footer background */
            color: white; /* White text */
            text-align: center;
            padding: 10px;
        }
        iframe {
            width: 100%;
            height: calc(100vh - 200px); /* Full height minus header and footer */
            border: none;
        }
    </style>
</head>
<body>

<header>
    <h1>Welcome to the Combined Page</h1>
</header>

<main>
    <div id="sidebar">
        <h3>Links</h3>
        <a href="#" onclick="loadPage('page1.html'); return false;">Page 1</a>
        <a href="#" onclick="loadPage('page2.html'); return false;">Page 2</a>
    </div>

    <div id="content">
        <iframe id="iframe" src="main-content.html"></iframe>
    </div>
</main>

<footer>
    <p>&copy; 2024 Your Company Name. All rights reserved.</p>
</footer>

<script>
    function loadPage(page) {
        document.getElementById('iframe').src = page;
    }

    // Load main content by default when the page loads
    window.onload = function() {
        loadPage('main-content.html'); // Replace 'main-content.html' with the path to your default content
    };
</script>

</body>
</html>





<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Main Content</title>
</head>
<body>
    <h1>Welcome!</h1>
    <p>This is the main content area. Click the links to load different content.</p>
    
    <h2>About This Site</h2>
    <p>This site demonstrates how to dynamically load content using JavaScript and the Fetch API. You can navigate through different sections without refreshing the page!</p>
    
    <h2>Features</h2>
    <ul>
        <li>Dynamic Content Loading</li>
        <li>Simple Navigation</li>
        <li>Responsive Design</li>
    </ul>
    
    <h2>Get Started</h2>
    <p>Click on the links in the sidebar to explore more.</p>
</body>
</html>

