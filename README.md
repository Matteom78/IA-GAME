<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Générateur d'Images IA - Recherche Intelligente</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            background: rgba(255, 255, 255, 0.98);
            border-radius: 25px;
            box-shadow: 0 25px 70px rgba(0, 0, 0, 0.3);
            max-width: 1400px;
            width: 100%;
            padding: 50px;
            margin: 0 auto;
        }

        .header {
            text-align: center;
            margin-bottom: 40px;
        }

        h1 {
            color: #667eea;
            margin-bottom: 15px;
            font-size: 3em;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.1);
        }

        .subtitle {
            color: #666;
            font-size: 1.2em;
            margin-bottom: 15px;
        }

        .badge {
            display: inline-block;
            background: linear-gradient(135deg, #4CAF50 0%, #45a049 100%);
            color: white;
            padding: 8px 20px;
            border-radius: 25px;
            font-size: 0.9em;
            margin: 5px;
            box-shadow: 0 4px 15px rgba(76, 175, 80, 0.3);
        }

        .ai-search-section {
            background: linear-gradient(135deg, #e3f2fd 0%, #f3e5f5 100%);
            border-radius: 20px;
            padding: 25px;
            margin-bottom: 30px;
            border: 2px solid #667eea;
            box-shadow: 0 8px 20px rgba(102, 126, 234, 0.2);
        }

        .ai-search-header h3 {
            color: #667eea;
            font-size: 1.3em;
            margin-bottom: 15px;
        }

        .search-input-group {
            display: flex;
            gap: 10px;
            margin-bottom: 15px;
        }

        .search-input {
            flex: 1;
            padding: 15px;
            border: 2px solid #667eea;
            border-radius: 12px;
            font-size: 16px;
        }

        .search-btn {
            padding: 15px 30px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border: none;
            border-radius: 12px;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
        }

        .search-btn:hover:not(:disabled) {
            transform: translateY(-2px);
            box-shadow: 0 8px 20px rgba(102, 126, 234, 0.4);
        }

        .search-btn:disabled {
            opacity: 0.6;
            cursor: not-allowed;
        }

        .search-results {
            background: white;
            border-radius: 12px;
            padding: 15px;
            margin-top: 15px;
            max-height: 300px;
            overflow-y: auto;
            display: none;
        }

        .search-results.active {
            display: block;
        }

        .search-result-item {
            padding: 10px;
            border-bottom: 1px solid #eee;
            color: #555;
            font-size: 14px;
            line-height: 1.6;
        }

        .input-section {
            margin-bottom: 30px;
        }

        textarea {
            width: 100%;
            padding: 20px;
            border: 3px solid #ddd;
            border-radius: 15px;
            font-size: 16px;
            resize: vertical;
            min-height: 120px;
            font-family: inherit;
        }

        .style-selector {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
            gap: 15px;
            margin: 20px 0;
        }

        .style-card {
            background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
            border: 3px solid transparent;
            border-radius: 15px;
            padding: 20px;
            text-align: center;
            cursor: pointer;
        }

        .style-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.15);
        }

        .style-card.active {
            border-color: #667eea;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
        }

        .style-card .emoji {
            font-size: 2.5em;
            margin-bottom: 10px;
            display: block;
        }

        .style-card .name {
            font-weight: bold;
            font-size: 1.1em;
        }

        .options {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-top: 20px;
        }

        .option-group {
            display: flex;
            flex-direction: column;
        }

        label {
            font-weight: bold;
            color: #555;
            margin-bottom: 8px;
            font-size: 15px;
        }

        select {
            padding: 12px;
            border: 2px solid #ddd;
            border-radius: 10px;
            font-size: 15px;
            cursor: pointer;
            background: white;
        }

        .button-group {
            display: flex;
            gap: 15px;
            margin-top: 20px;
        }

        button {
            flex: 1;
            padding: 18px 35px;
            font-size: 18px;
            font-weight: bold;
            border: none;
            border-radius: 12px;
            cursor: pointer;
        }

        .generate-btn {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            box-shadow: 0 6px 20px rgba(102, 126, 234, 0.4);
        }

        .generate-btn:hover:not(:disabled) {
            transform: translateY(-3px);
            box-shadow: 0 12px 30px rgba(102, 126, 234, 0.5);
        }

        .generate-btn:disabled {
            opacity: 0.6;
            cursor: not-allowed;
        }

        .clear-btn {
            background: linear-gradient(135deg, #f44336 0%, #e91e63 100%);
            color: white;
            flex: 0.3;
        }

        .clear-btn:hover {
            transform: translateY(-3px);
        }

        .loading {
            text-align: center;
            margin: 30px 0;
            color: #667eea;
            font-size: 20px;
            display: none;
        }

        .loading.active {
            display: block;
        }

        .spinner {
            border: 5px solid #f3f3f3;
            border-top: 5px solid #667eea;
            border-radius: 50%;
            width: 50px;
            height: 50px;
            animation: spin 1s linear infinite;
            margin: 0 auto 15px;
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        .gallery {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
            gap: 25px;
            margin-top: 40px;
        }

        .image-card {
            background: white;
            border-radius: 20px;
            overflow: hidden;
            box-shadow: 0 8px 25px rgba(0, 0, 0, 0.1);
        }

        .image-card:hover {
            transform: translateY(-8px);
            box-shadow: 0 15px 40px rgba(0, 0, 0, 0.2);
        }

        .image-wrapper {
            width: 100%;
            height: 320px;
            overflow: hidden;
            background: linear-gradient(135deg, #f0f0f0 0%, #e0e0e0 100%);
            position: relative;
        }

        .image-card img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }

        .image-loading {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
        }

        .image-info {
            padding: 20px;
        }

        .image-prompt {
            font-size: 15px;
            color: #666;
            margin-bottom: 12px;
            display: -webkit-box;
            -webkit-line-clamp: 2;
            -webkit-box-orient: vertical;
            overflow: hidden;
            line-height: 1.5;
        }

        .image-style-tag {
            display: inline-block;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 5px 12px;
            border-radius: 15px;
            font-size: 12px;
            margin-bottom: 10px;
        }

        .image-actions {
            display: flex;
            gap: 10px;
        }

        .action-btn {
            flex: 1;
            padding: 12px;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-size: 15px;
            font-weight: bold;
        }

        .download-btn {
            background: linear-gradient(135deg, #4CAF50 0%, #45a049 100%);
            color: white;
        }

        .download-btn:hover {
            transform: translateY(-2px);
        }

        .view-btn {
            background: linear-gradient(135deg, #2196F3 0%, #0b7dda 100%);
            color: white;
        }

        .view-btn:hover {
            transform: translateY(-2px);
        }

        .counter {
            text-align: center;
            margin: 30px 0;
            font-size: 22px;
            color: #667eea;
            font-weight: bold;
        }

        .error {
            background: linear-gradient(135deg, #ffebee 0%, #ffcdd2 100%);
            color: #c62828;
            padding: 20px;
            border-radius: 15px;
            margin: 20px 0;
            display: none;
            border-left: 5px solid #c62828;
        }

        .error.active {
            display: block;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>🎨 Générateur d'Images IA Intelligent</h1>
            <p class="subtitle">Recherche Google + Génération illimitée</p>
            <div>
                <span class="badge">✨ GRATUIT</span>
                <span class="badge">🔍 RECHERCHE IA</span>
                <span class="badge">🎯 MULTI-STYLES</span>
            </div>
        </div>

        <div class="ai-search-section">
            <div class="ai-search-header">
                <h3>🔍 Recherche Intelligente</h3>
            </div>
            <p style="color: #666; margin-bottom: 15px; font-size: 14px;">
                <strong>🤖 IA Boostée par Claude + Recherche Web Réelle !</strong><br>
                L'IA va chercher des informations actuelles sur Google pour enrichir votre prompt avec des détails réalistes et précis !
            </p>
            <div class="search-input-group">
                <input type="text" class="search-input" id="searchInput" placeholder="Ex: Tour Eiffel, Dragon japonais, Lamborghini, Chat mignon...">
                <button class="search-btn" id="searchBtn">🔍 Rechercher</button>
            </div>
            <div class="search-results" id="searchResults"></div>
        </div>

        <div class="input-section">
            <textarea id="promptInput" placeholder="Décris l'image que tu veux créer en détail...

💡 Astuce: Utilise la recherche ci-dessus pour obtenir des détails précis, puis complète ici avec ton style !

Exemples:
- Un chat astronaute flottant dans l'espace avec des étoiles colorées
- Un dragon majestueux sur une montagne enneigée au coucher du soleil
- Une ville futuriste avec des voitures volantes et des gratte-ciels lumineux"></textarea>
            
            <div style="margin: 20px 0;">
                <label style="display: block; margin-bottom: 15px; font-size: 18px; color: #667eea;">🎨 Choisis ton style:</label>
                <div class="style-selector">
                    <div class="style-card active" data-style="flux">
                        <span class="emoji">⚡</span>
                        <span class="name">Standard</span>
                    </div>
                    <div class="style-card" data-style="flux-realism">
                        <span class="emoji">📸</span>
                        <span class="name">Réaliste</span>
                    </div>
                    <div class="style-card" data-style="flux-anime">
                        <span class="emoji">🎌</span>
                        <span class="name">Anime</span>
                    </div>
                    <div class="style-card" data-style="flux-3d">
                        <span class="emoji">🎮</span>
                        <span class="name">3D</span>
                    </div>
                    <div class="style-card" data-style="flux-pro">
                        <span class="emoji">💎</span>
                        <span class="name">Pro</span>
                    </div>
                    <div class="style-card" data-style="turbo">
                        <span class="emoji">🚀</span>
                        <span class="name">Rapide</span>
                    </div>
                </div>
            </div>

            <div class="options">
                <div class="option-group">
                    <label for="width">📏 Largeur</label>
                    <select id="width">
                        <option value="512">512px - Rapide</option>
                        <option value="768">768px - Moyen</option>
                        <option value="1024" selected>1024px - Standard</option>
                        <option value="1280">1280px - Haute Qualité</option>
                    </select>
                </div>
                <div class="option-group">
                    <label for="height">📐 Hauteur</label>
                    <select id="height">
                        <option value="512">512px - Rapide</option>
                        <option value="768">768px - Moyen</option>
                        <option value="1024" selected>1024px - Standard</option>
                        <option value="1280">1280px - Haute Qualité</option>
                    </select>
                </div>
                <div class="option-group">
                    <label for="seed">🎲 Seed (Optionnel)</label>
                    <select id="seed">
                        <option value="">Aléatoire</option>
                        <option value="42">42 - Reproductible</option>
                        <option value="123">123</option>
                        <option value="777">777</option>
                    </select>
                </div>
            </div>

            <div class="button-group">
                <button class="generate-btn" id="generateBtn">✨ Générer l'Image</button>
                <button class="clear-btn" id="clearBtn">🗑️ Effacer</button>
            </div>
        </div>

        <div class="loading" id="loading">
            <div class="spinner"></div>
            <p>Génération de ton image en cours...</p>
        </div>

        <div class="error" id="error"></div>

        <div class="counter" id="counter">0 images générées</div>

        <div class="gallery" id="gallery"></div>
    </div>

    <script>
        console.log('🎨 Initialisation du générateur d\'images IA...');
        
        const promptInput = document.getElementById('promptInput');
        const generateBtn = document.getElementById('generateBtn');
        const clearBtn = document.getElementById('clearBtn');
        const loading = document.getElementById('loading');
        const gallery = document.getElementById('gallery');
        const errorDiv = document.getElementById('error');
        const counter = document.getElementById('counter');
        const widthSelect = document.getElementById('width');
        const heightSelect = document.getElementById('height');
        const seedSelect = document.getElementById('seed');
        const styleCards = document.querySelectorAll('.style-card');
        const searchInput = document.getElementById('searchInput');
        const searchBtn = document.getElementById('searchBtn');
        const searchResults = document.getElementById('searchResults');

        let imageCount = 0;
        let selectedStyle = 'flux';

        console.log('✅ Éléments chargés');

        styleCards.forEach(card => {
            card.addEventListener('click', function() {
                console.log('Style card cliqué');
                styleCards.forEach(c => c.classList.remove('active'));
                this.classList.add('active');
                selectedStyle = this.dataset.style;
                console.log('Style sélectionné:', selectedStyle);
            });
        });

        searchBtn.addEventListener('click', function() {
            console.log('Bouton recherche cliqué');
            performSearch();
        });

        searchInput.addEventListener('keypress', (e) => {
            if (e.key === 'Enter') {
                e.preventDefault();
                performSearch();
            }
        });

        async function performSearch() {
            const query = searchInput.value.trim();
            
            if (!query) {
                showError('⚠️ Merci d\'entrer un terme de recherche !');
                return;
            }

            searchBtn.disabled = true;
            searchResults.innerHTML = `
                <div style="text-align: center; padding: 20px;">
                    <div class="spinner"></div>
                    <p style="margin-top: 15px;">🔍 Recherche IA en cours...</p>
                </div>
            `;
            searchResults.classList.add('active');

            try {
                console.log('Recherche pour:', query);
                const enrichedPrompt = await enrichPromptWithSearch(query);
                
                promptInput.value = enrichedPrompt;
                
                searchResults.innerHTML = `
                    <div class="search-result-item">
                        <strong style="color: #4CAF50;">✅ Recherche IA terminée !</strong><br>
                        <p style="margin: 10px 0;">Votre prompt a été enrichi.</p>
                    </div>
                `;
                
                setTimeout(() => {
                    searchResults.classList.remove('active');
                }, 4000);
                
            } catch (error) {
                console.error('Erreur:', error);
                const fallbackPrompt = createFallbackPrompt(query);
                promptInput.value = fallbackPrompt;
                
                searchResults.innerHTML = `
                    <div class="search-result-item">
                        <strong style="color: #ff9800;">⚠️ Mode de secours</strong><br>
                        Un prompt enrichi a été créé pour vous.
                    </div>
                `;
                
                setTimeout(() => {
                    searchResults.classList.remove('active');
                }, 4000);
            } finally {
                searchBtn.disabled = false;
            }
        }

        async function enrichPromptWithSearch(query) {
            try {
                const response = await fetch("https://api.anthropic.com/v1/messages", {
                    method: "POST",
                    headers: {
                        "Content-Type": "application/json",
                    },
                    body: JSON.stringify({
                        model: "claude-sonnet-4-20250514",
                        max_tokens: 1000,
                        tools: [{
                            type: "web_search_20250305",
                            name: "web_search"
                        }],
                        messages: [{
                            role: "user",
                            content: `Je veux créer une image de: "${query}". Recherche sur le web et crée un prompt détaillé en français pour un générateur d'images IA. Réponds UNIQUEMENT avec le prompt enrichi, sans introduction.`
                        }]
                    })
                });

                const data = await response.json();
                
                let enrichedPrompt = data.content
                    .filter(item => item.type === "text")
                    .map(item => item.text)
                    .join(" ")
                    .trim();

                if (enrichedPrompt.length < 20) {
                    return createFallbackPrompt(query);
                }

                return enrichedPrompt;

            } catch (error) {
                console.error('Erreur API:', error);
                return createFallbackPrompt(query);
            }
        }

        function createFallbackPrompt(query) {
            const enrichments = {
                'chat': 'un magnifique chat aux yeux expressifs, fourrure détaillée, éclairage doux et chaleureux',
                'dragon': 'un dragon majestueux avec des écailles brillantes, ailes déployées, flammes mystiques',
                'tour eiffel': 'la Tour Eiffel à Paris, architecture détaillée, ciel coloré au coucher du soleil',
                'voiture': 'une voiture de sport luxueuse, carrosserie brillante, éclairage dynamique professionnel',
                'paysage': 'un paysage naturel époustouflant, lumière cinématographique, détails naturels riches'
            };

            for (const [key, value] of Object.entries(enrichments)) {
                if (query.toLowerCase().includes(key)) {
                    return value;
                }
            }

            return `${query}, haute qualité, détails précis, éclairage professionnel, composition artistique`;
        }

        generateBtn.addEventListener('click', function() {
            console.log('Bouton générer cliqué');
            generateImage();
        });

        clearBtn.addEventListener('click', function() {
            console.log('Bouton effacer cliqué');
            clearGallery();
        });

        promptInput.addEventListener('keypress', (e) => {
            if (e.key === 'Enter' && !e.shiftKey) {
                e.preventDefault();
                generateImage();
            }
        });

        async function generateImage() {
            const prompt = promptInput.value.trim();
            
            if (!prompt) {
                showError('⚠️ Merci de décrire l\'image !');
                return;
            }

            console.log('Génération pour:', prompt);
            
            hideError();
            loading.classList.add('active');
            generateBtn.disabled = true;

            try {
                const width = widthSelect.value;
                const height = heightSelect.value;
                const seed = seedSelect.value;
                
                const encodedPrompt = encodeURIComponent(prompt);
                
                let imageUrl = `https://image.pollinations.ai/prompt/${encodedPrompt}?width=${width}&height=${height}&model=${selectedStyle}&nologo=true&enhance=true&timestamp=${Date.now()}`;
                
                if (seed) {
                    imageUrl += `&seed=${seed}`;
                }
                
                addImageToGallery(imageUrl, prompt, selectedStyle);
                imageCount++;
                updateCounter();
                
                promptInput.value = '';
                console.log('✅ Image générée');

            } catch (error) {
                console.error('Erreur:', error);
                showError('😢 Oups ! Une erreur est survenue.');
            } finally {
                loading.classList.remove('active');
                generateBtn.disabled = false;
            }
        }

        function addImageToGallery(imageUrl, prompt, style) {
            const styleNames = {
                'flux': 'Standard',
                'flux-realism': 'Réaliste',
                'flux-anime': 'Anime',
                'flux-3d': '3D',
                'flux-pro': 'Pro',
                'turbo': 'Rapide'
            };

            const imageCard = document.createElement('div');
            imageCard.className = 'image-card';
            
            imageCard.innerHTML = `
                <div class="image-wrapper">
                    <div class="image-loading">
                        <div class="spinner"></div>
                    </div>
                    <img data-src="${imageUrl}" alt="${prompt}" style="display: none;">
                </div>
                <div class="image-info">
                    <div class="image-style-tag">${styleNames[style] || style}</div>
                    <div class="image-prompt">${prompt}</div>
                    <div class="image-actions">
                        <button class="action-btn download-btn">⬇️ Télécharger</button>
                        <button class="action-btn view-btn">👁️ Voir</button>
                    </div>
                </div>
            `;
            
            const img = imageCard.querySelector('img');
            const loadingDiv = imageCard.querySelector('.image-loading');
            const downloadBtn = imageCard.querySelector('.download-btn');
            const viewBtn = imageCard.querySelector('.view-btn');
            
            img.onload = () => {
                loadingDiv.style.display = 'none';
                img.style.display = 'block';
            };
            
            img.onerror = () => {
                loadingDiv.innerHTML = '<p style="color: #f44336;">❌ Erreur</p>';
            };
            
            setTimeout(() => {
                img.src = img.dataset.src;
            }, 100);
            
            downloadBtn.addEventListener('click', () => downloadImage(imageUrl, prompt));
            viewBtn.addEventListener('click', () => window.open(imageUrl, '_blank'));
            
            gallery.insertBefore(imageCard, gallery.firstChild);
        }

        async function downloadImage(url, prompt) {
            try {
                const response = await fetch(url);
                const blob = await response.blob();
                const blobUrl = URL.createObjectURL(blob);
                
                const a = document.createElement('a');
                a.href = blobUrl;
                a.download = `image_${Date.now()}.png`;
                document.body.appendChild(a);
                a.click();
                document.body.removeChild(a);
                URL.revokeObjectURL(blobUrl);
                
            } catch (error) {
                console.error('Erreur téléchargement:', error);
                showError('❌ Erreur de téléchargement.');
            }
        }

        function clearGallery() {
            if (imageCount === 0) {
                showError('ℹ️ La galerie est déjà vide !');
                return;
            }
            
            if (confirm(`Effacer les ${imageCount} images ?`)) {
                gallery.innerHTML = '';
                imageCount = 0;
                updateCounter();
            }
        }

        function updateCounter() {
            if (imageCount === 0) {
                counter.textContent = 'Aucune image générée';
            } else {
                counter.textContent = `${imageCount} image${imageCount > 1 ? 's' : ''} générée${imageCount > 1 ? 's' : ''}`;
            }
        }

        function showError(message) {
            errorDiv.textContent = message;
            errorDiv.classList.add('active');
            setTimeout(() => hideError(), 5000);
        }

        function hideError() {
            errorDiv.classList.remove('active');
        }

        console.log('✅ Application prête !');
    </script>
</body>
</html>
