
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>News by Theme</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f4f4f9;
        }
        header {
            background: #333;
            color: white;
            padding: 10px 20px;
            text-align: center;
        }
        #theme-selector {
            margin: 20px auto;
            display: block;
            width: 50%;
            padding: 10px;
            font-size: 16px;
        }
        .news-container {
            max-width: 800px;
            margin: 20px auto;
            background: white;
            padding: 20px;
            border-radius: 5px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        .article {
            margin-bottom: 20px;
            padding-bottom: 10px;
            border-bottom: 1px solid #ccc;
        }
        .article h3 {
            margin: 0 0 10px;
        }
        .article a {
            color: #0066cc;
            text-decoration: none;
        }
        .article a:hover {
            text-decoration: underline;
        }
    </style>
</head>
<body>
    <header>
        <h1>News by Theme</h1>
    </header>
    <select id="theme-selector">
        <option value="technology">Technology</option>
        <option value="health">Health</option>
        <option value="sports">Sports</option>
        <option value="business">Business</option>
        <option value="entertainment">Entertainment</option>
    </select>
    <div id="news-container" class="news-container"></div>

    <script>
        const apiKey = 'ea87e7dcf48e4e9f8f9297bef222624a'; // Remplacez par votre clé NewsAPI
        const newsContainer = document.getElementById('news-container');
        const themeSelector = document.getElementById('theme-selector');

        // Fonction pour charger les actualités
        const fetchNews = (theme) => {
            const url = `https://newsapi.org/v2/top-headlines?category=${theme}&language=en&apiKey=${apiKey}`;
            newsContainer.innerHTML = '<p>Loading news...</p>';
            fetch(url)
                .then(response => response.json())
                .then(data => {
                    newsContainer.innerHTML = '';
                    if (data.articles.length === 0) {
                        newsContainer.innerHTML = '<p>No news found for this category.</p>';
                    }
                    data.articles.forEach(article => {
                        const newsHTML = `
                            <div class="article">
                                <h3>${article.title}</h3>
                                <p>${article.description || 'No description available.'}</p>
                                <a href="${article.url}" target="_blank">Read more</a>
                            </div>
                        `;
                        newsContainer.innerHTML += newsHTML;
                    });
                })
                .catch(error => {
                    newsContainer.innerHTML = '<p>Error loading news. Please try again later.</p>';
                    console.error('Error fetching news:', error);
                });
        };

        // Charger les actualités par défaut
        fetchNews('technology');

        // Changer le thème des actualités
        themeSelector.addEventListener('change', (event) => {
            fetchNews(event.target.value);
        });
    </script>
</body>
</html>
