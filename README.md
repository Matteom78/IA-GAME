<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Assistant IA - Recherche & Code</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @keyframes spin {
            from { transform: rotate(0deg); }
            to { transform: rotate(360deg); }
        }
        .animate-spin {
            animation: spin 1s linear infinite;
        }
        .gradient-bg {
            background: linear-gradient(135deg, #1e293b 0%, #581c87 50%, #1e293b 100%);
        }
        .message-enter {
            animation: slideIn 0.3s ease-out;
        }
        @keyframes slideIn {
            from {
                opacity: 0;
                transform: translateY(10px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
    </style>
</head>
<body class="gradient-bg min-h-screen p-4">
    <div class="max-w-5xl mx-auto h-[90vh] bg-slate-800/50 backdrop-blur-xl rounded-3xl shadow-2xl border border-purple-500/20 flex flex-col overflow-hidden">
        
        <!-- Header -->
        <div style="background: linear-gradient(90deg, #9333ea, #ec4899);" class="p-6">
            <div class="flex items-center gap-4">
                <div class="bg-white/20 p-3 rounded-xl backdrop-blur-sm">
                    <svg class="w-8 h-8 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 3v4M3 5h4M6 17v4m-2-2h4m5-16l2.286 6.857L21 12l-5.714 2.143L13 21l-2.286-6.857L5 12l5.714-2.143L13 3z"/>
                    </svg>
                </div>
                <div class="flex-1">
                    <h1 class="text-2xl font-bold text-white">Assistant IA</h1>
                    <div class="flex items-center gap-4 mt-1">
                        <span class="flex items-center gap-1 text-purple-100 text-sm">
                            <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 12a9 9 0 01-9 9m9-9a9 9 0 00-9-9m9 9H3m9 9a9 9 0 01-9-9m9 9c1.657 0 3-4.03 3-9s-1.343-9-3-9m0 18c-1.657 0-3-4.03-3-9s1.343-9 3-9m-9 9a9 9 0 019-9"/>
                            </svg>
                            Recherche Web
                        </span>
                        <span class="flex items-center gap-1 text-purple-100 text-sm">
                            <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 20l4-16m4 4l4 4-4 4M6 16l-4-4 4-4"/>
                            </svg>
                            Expert Code
                        </span>
                    </div>
                </div>
            </div>
        </div>

        <!-- Messages Container -->
        <div id="messagesContainer" class="flex-1 overflow-y-auto p-6 space-y-4">
            <!-- Welcome Message -->
            <div id="welcomeMessage" class="text-center text-gray-400 mt-20">
                <svg class="w-16 h-16 mx-auto mb-4 text-purple-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 3v4M3 5h4M6 17v4m-2-2h4m5-16l2.286 6.857L21 12l-5.714 2.143L13 21l-2.286-6.857L5 12l5.714-2.143L13 3z"/>
                </svg>
                <h2 class="text-2xl font-bold mb-2 text-white">Bonjour ! 👋</h2>
                <p class="mb-6">Je suis ton assistant IA avec accès à la recherche web.</p>
                <div class="grid grid-cols-1 md:grid-cols-2 gap-4 max-w-2xl mx-auto text-left">
                    <div class="bg-slate-700/50 p-4 rounded-xl border border-purple-500/20">
                        <svg class="w-6 h-6 text-purple-400 mb-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 12a9 9 0 01-9 9m9-9a9 9 0 00-9-9m9 9H3m9 9a9 9 0 01-9-9m9 9c1.657 0 3-4.03 3-9s-1.343-9-3-9m0 18c-1.657 0-3-4.03-3-9s1.343-9 3-9m-9 9a9 9 0 019-9"/>
                        </svg>
                        <p class="text-sm text-gray-300">Recherche des infos actuelles sur le web</p>
                    </div>
                    <div class="bg-slate-700/50 p-4 rounded-xl border border-purple-500/20">
                        <svg class="w-6 h-6 text-pink-400 mb-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 20l4-16m4 4l4 4-4 4M6 16l-4-4 4-4"/>
                        </svg>
                        <p class="text-sm text-gray-300">Génère du code dans tous les langages</p>
                    </div>
                </div>
            </div>
        </div>

        <!-- Input Area -->
        <div class="p-6 bg-slate-800/80 border-t border-slate-700">
            <div class="flex gap-3">
                <input
                    type="text"
                    id="userInput"
                    placeholder="Pose-moi une question ou demande-moi de coder quelque chose..."
                    class="flex-1 bg-slate-700 text-white rounded-xl px-6 py-4 focus:outline-none focus:ring-2 focus:ring-purple-500 border border-slate-600"
                />
                <button
                    id="sendButton"
                    style="background: linear-gradient(90deg, #9333ea, #ec4899);"
                    class="text-white rounded-xl px-8 py-4 font-semibold hover:opacity-90 transition-all duration-200 flex items-center gap-2 shadow-lg hover:shadow-xl"
                >
                    <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 19l9 2-9-18-9 18 9-2zm0 0v-8"/>
                    </svg>
                    Envoyer
                </button>
            </div>
        </div>
    </div>

    <script>
        let conversationHistory = [];
        let isLoading = false;

        const messagesContainer = document.getElementById('messagesContainer');
        const userInput = document.getElementById('userInput');
        const sendButton = document.getElementById('sendButton');
        const welcomeMessage = document.getElementById('welcomeMessage');

        function scrollToBottom() {
            messagesContainer.scrollTop = messagesContainer.scrollHeight;
        }

        function formatCodeBlocks(text) {
            return text.replace(/```(\w+)?\n([\s\S]*?)```/g, (match, lang, code) => {
                return `<pre class="bg-slate-900 p-4 rounded-lg my-2 overflow-x-auto">
                    <div class="text-xs text-purple-400 mb-2">${lang || 'code'}</div>
                    <code class="text-sm text-gray-300">${escapeHtml(code.trim())}</code>
                </pre>`;
            });
        }

        function escapeHtml(text) {
            const div = document.createElement('div');
            div.textContent = text;
            return div.innerHTML;
        }

        function addMessage(role, content, isSearching = false) {
            if (welcomeMessage && welcomeMessage.parentElement) {
                welcomeMessage.remove();
            }

            const messageDiv = document.createElement('div');
            messageDiv.className = `flex message-enter ${role === 'user' ? 'justify-end' : 'justify-start'}`;
            
            let bgClass, textClass;
            if (role === 'user') {
                bgClass = 'bg-gradient-to-r from-purple-600 to-pink-600';
                textClass = 'text-white';
            } else if (isSearching) {
                bgClass = 'bg-blue-500/20 border border-blue-500/30';
                textClass = 'text-blue-300';
            } else {
                bgClass = 'bg-slate-700/50 border border-slate-600/50';
                textClass = 'text-gray-100';
            }

            const formattedContent = role === 'assistant' && !isSearching 
                ? formatCodeBlocks(content)
                : escapeHtml(content);

            messageDiv.innerHTML = `
                <div class="max-w-[80%] rounded-2xl p-4 ${bgClass} ${textClass}">
                    <div class="whitespace-pre-wrap break-words">${formattedContent}</div>
                </div>
            `;

            messagesContainer.appendChild(messageDiv);
            scrollToBottom();
            
            return messageDiv;
        }

        function addLoadingIndicator() {
            const loadingDiv = document.createElement('div');
            loadingDiv.id = 'loadingIndicator';
            loadingDiv.className = 'flex justify-start message-enter';
            loadingDiv.innerHTML = `
                <div class="bg-slate-700/50 rounded-2xl p-4 border border-slate-600/50">
                    <svg class="w-6 h-6 text-purple-400 animate-spin" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 4v5h.582m15.356 2A8.001 8.001 0 004.582 9m0 0H9m11 11v-5h-.581m0 0a8.003 8.003 0 01-15.357-2m15.357 2H15"/>
                    </svg>
                </div>
            `;
            messagesContainer.appendChild(loadingDiv);
            scrollToBottom();
            return loadingDiv;
        }

        async function sendMessage() {
            if (isLoading || !userInput.value.trim()) return;

            const message = userInput.value.trim();
            userInput.value = '';
            isLoading = true;
            sendButton.disabled = true;
            sendButton.style.opacity = '0.5';

            addMessage('user', message);

            const loadingIndicator = addLoadingIndicator();

            try {
                // Construction des messages pour l'historique
                const messages = conversationHistory.concat([
                    { role: 'user', content: message }
                ]);

                const response = await fetch("https://api.anthropic.com/v1/messages", {
                    method: "POST",
                    headers: {
                        "Content-Type": "application/json",
                        "anthropic-version": "2023-06-01"
                    },
                    body: JSON.stringify({
                        model: "claude-sonnet-4-20250514",
                        max_tokens: 4000,
                        system: `Tu es un assistant IA expert en programmation. Tu as accès à la recherche web pour trouver des informations actuelles.

Capacités:
- Utilise l'outil web_search pour chercher des informations sur Internet quand nécessaire
- Tu es expert en tous les langages de programmation
- Tu donnes des explications claires et du code de qualité
- Tu utilises la recherche web pour trouver des solutions à jour, des documentations, ou vérifier des informations

Quand utiliser la recherche web:
- Pour trouver des informations récentes (versions de librairies, nouvelles API, etc.)
- Pour vérifier la documentation officielle
- Pour trouver des solutions à des problèmes spécifiques
- Pour découvrir les meilleures pratiques actuelles

Réponds toujours en français de manière claire et professionnelle.`,
                        messages: messages,
                        tools: [{
                            type: "web_search_20250305",
                            name: "web_search"
                        }]
                    })
                });

                if (!response.ok) {
                    throw new Error(`Erreur API: ${response.status}`);
                }

                const data = await response.json();
                
                let fullResponse = '';
                let hasToolUse = false;
                
                for (const block of data.content) {
                    if (block.type === 'text') {
                        fullResponse += block.text;
                    } else if (block.type === 'tool_use') {
                        hasToolUse = true;
                        loadingIndicator.remove();
                        addMessage('assistant', '🔍 Recherche en cours sur le web...', true);
                    }
                }

                if (hasToolUse && data.stop_reason === 'tool_use') {
                    const toolResults = data.content
                        .filter(block => block.type === 'tool_use')
                        .map(block => ({
                            type: "tool_result",
                            tool_use_id: block.id,
                            content: "Recherche effectuée avec succès."
                        }));

                    conversationHistory.push({ role: 'user', content: message });
                    conversationHistory.push({ role: 'assistant', content: data.content });
                    conversationHistory.push({ role: 'user', content: toolResults });

                    const followUpResponse = await fetch("https://api.anthropic.com/v1/messages", {
                        method: "POST",
                        headers: {
                            "Content-Type": "application/json",
                            "anthropic-version": "2023-06-01"
                        },
                        body: JSON.stringify({
                            model: "claude-sonnet-4-20250514",
                            max_tokens: 4000,
                            system: `Tu es un assistant IA expert en programmation avec accès à la recherche web.`,
                            messages: conversationHistory
                        })
                    });

                    const followUpData = await followUpResponse.json();
                    fullResponse = followUpData.content
                        .filter(block => block.type === 'text')
                        .map(block => block.text)
                        .join('\n');

                    // Retirer le message de recherche
                    const searchMessages = messagesContainer.querySelectorAll('.bg-blue-500\\/20');
                    searchMessages.forEach(msg => msg.parentElement.remove());
                } else {
                    conversationHistory.push({ role: 'user', content: message });
                    conversationHistory.push({ role: 'assistant', content: fullResponse });
                }

                loadingIndicator.remove();
                addMessage('assistant', fullResponse);

            } catch (error) {
                loadingIndicator.remove();
                addMessage('assistant', `❌ Erreur: Cette application nécessite d'être exécutée dans claude.ai pour fonctionner correctement. L'API Anthropic requiert une authentification qui ne peut être gérée côté client pour des raisons de sécurité.\n\nPour utiliser cette fonctionnalité, vous devez :\n1. Utiliser cette application directement dans claude.ai (artifacts)\n2. Ou créer un backend serveur pour gérer l'authentification API`);
            } finally {
                isLoading = false;
                sendButton.disabled = false;
                sendButton.style.opacity = '1';
                userInput.focus();
            }
        }

        sendButton.addEventListener('click', sendMessage);
        userInput.addEventListener('keypress', (e) => {
            if (e.key === 'Enter' && !e.shiftKey) {
                e.preventDefault();
                sendMessage();
            }
        });

        // Focus input on load
        userInput.focus();
    </script>
</body>
</html>
