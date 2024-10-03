<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dynamic Content Loading</title>
    <style>
        body {
            display: flex;
            margin: 0;
            font-family: Arial, sans-serif;
            height: 100vh;
            background-color: #eaeaea;
        }
        .sidebar {
            width: 250px;
            background-color: #4a90e2;
            color: white;
            padding: 10px; /* Reduced padding */
            box-shadow: 2px 0 5px rgba(0, 0, 0, 0.3);
            display: flex;
            flex-direction: column; /* Stack items vertically */
            justify-content: flex-start; /* Align links to the top */
        }
        .link {
            display: block;
            margin: 5px 0; /* Reduced margin */
            text-decoration: none;
            color: white;
            padding: 10px; /* Adjusted padding */
            border-radius: 5px;
            transition: background-color 0.3s, transform 0.2s;
        }
        .link:hover {
            background-color: #357ab8;
            transform: scale(1.05);
        }
        .content {
            flex-grow: 1;
            padding: 30px;
            background-color: white;
            overflow: auto;
            transition: background-color 0.3s;
        }
        .content h1, .content h2 {
            color: #333;
        }
        img {
            display: block;
            margin: 20px auto;
            max-width: 100%;
            height: auto;
            border-radius: 8px;
        }
        .loader {
            text-align: center;
        }
        .loader::after {
            content: '';
            border: 5px solid #ccc;
            border-top: 5px solid #3498db;
            border-radius: 50%;
            width: 30px;
            height: 30px;
            animation: spin 1s linear infinite;
        }
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
    </style>
    <script>
        function loadContent(page) {
            const contentArea = document.getElementById('content-area');
            contentArea.innerHTML = '<div class="loader"></div>'; // Show loading animation
            fetch(page)
                .then(response => {
                    if (!response.ok) throw new Error('Network response was not ok');
                    return response.text();
                })
                .then(data => {
                    contentArea.innerHTML = data;
                })
                .catch(error => {
                    contentArea.innerHTML = '<p>Error loading content. Please try again later.</p>';
                    console.error('Error fetching the page:', error);
                });
        }
    </script>
</head>
<body>

    <nav class="sidebar" role="navigation">
        <h2>Navigation</h2>
        <a href="#" class="link" onclick="loadContent('index.html'); return false;">Link 1</a>
        <a href="#" class="link" onclick="loadContent('page2.html'); return false;">Link 2</a>
    </nav>

    <main class="content" id="content-area">
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
        
        <img src="https://via.placeholder.com/400" alt="Placeholder Image">
    </main>

</body>
</html>
