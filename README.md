# mindflow.ai-ou-mindflow.chat
Nicassino08@gmail.com<!DOCTYPE html>
<html lang="pt-pt">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Floricultura Azul - Vídeo Automático</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600&display=swap');
        body { font-family: 'Poppins', sans-serif; background-color: #f0f9ff; }
        
        .video-container {
            position: relative;
            border: 8px solid #1e40af;
            border-radius: 1.5rem;
            overflow: hidden;
            box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.2);
            background: #000;
        }

        /* Animação de pulso para o botão de play se o vídeo não iniciar */
        .pulse-button {
            animation: pulse 2s infinite;
        }
        @keyframes pulse {
            0% { transform: scale(1); box-shadow: 0 0 0 0 rgba(59, 130, 246, 0.7); }
            70% { transform: scale(1.05); box-shadow: 0 0 0 10px rgba(59, 130, 246, 0); }
            100% { transform: scale(1); box-shadow: 0 0 0 0 rgba(59, 130, 246, 0); }
        }
    </style>
</head>
<body class="pb-12 text-gray-800">

    <header class="bg-blue-800 text-white py-10 px-4 text-center shadow-md mb-8">
        <h1 class="text-3xl md:text-4xl font-bold">Floricultura Azul</h1>
        <p class="text-blue-100 mt-2">O seu jardim digital em movimento</p>
    </header>

    <main class="max-w-3xl mx-auto px-4">
        
        <!-- Alerta de Status -->
        <div id="statusAlert" class="hidden mb-4 p-4 rounded-xl bg-yellow-100 border border-yellow-300 text-yellow-800 text-sm text-center">
            O vídeo está a demorar a carregar. Verifique se o ficheiro está na mesma pasta que este site.
        </div>

        <!-- Contentor do Vídeo -->
        <div class="video-container group">
            <!-- Adicionado 'autoplay', 'muted' e 'playsinline' para garantir o início automático -->
            <video id="meuVideo" 
                   class="w-full h-auto" 
                   autoplay 
                   muted 
                   loop 
                   playsinline 
                   controls
                   poster="https://images.unsplash.com/photo-1526047932273-341f2a7631f9?w=800">
                <source src="grok_video_2026-02-01-15-47-47.mp4" type="video/mp4">
                O seu navegador não suporta vídeos.
            </video>

            <!-- Overlay de Play Manual (caso o autoplay falhe) -->
            <div id="playOverlay" class="absolute inset-0 flex items-center justify-center bg-black bg-opacity-50 transition-opacity duration-500">
                <button onclick="forçarPlay()" class="pulse-button bg-blue-600 hover:bg-blue-700 text-white font-bold py-4 px-8 rounded-full flex items-center gap-3 shadow-2xl">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14.752 11.168l-3.197-2.132A1 1 0 0010 9.87v4.263a1 1 0 001.555.832l3.197-2.132a1 1 0 000-1.664z" />
                    </svg>
                    REPRODUZIR AGORA
                </button>
            </div>
        </div>

        <div class="mt-6 text-center">
            <button onclick="ativarSom()" class="text-blue-700 font-semibold flex items-center justify-center mx-auto gap-2 hover:underline">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15.536 8.464a5 5 0 010 7.072m2.828-9.9a9 9 0 010 12.728M5.586 15H4a1 1 0 01-1-1v-4a1 1 0 011-1h1.586l4.707-4.707C10.923 3.663 12 4.109 12 5v14c0 .891-1.077 1.337-1.707.707L5.586 15z" />
                </svg>
                Ativar Som das Flores
            </button>
        </div>

        <div class="grid grid-cols-3 gap-4 mt-12">
            <div class="bg-white p-4 rounded-xl shadow-sm text-center border border-blue-50">
                <span class="text-3xl">🌸</span>
                <p class="text-xs font-bold mt-2 uppercase">Lírios</p>
            </div>
            <div class="bg-white p-4 rounded-xl shadow-sm text-center border border-blue-50">
                <span class="text-3xl">🌹</span>
                <p class="text-xs font-bold mt-2 uppercase">Rosas</p>
            </div>
            <div class="bg-white p-4 rounded-xl shadow-sm text-center border border-blue-50">
                <span class="text-3xl">🌻</span>
                <p class="text-xs font-bold mt-2 uppercase">Girassóis</p>
            </div>
        </div>
    </main>

    <script>
        const video = document.getElementById('meuVideo');
        const overlay = document.getElementById('playOverlay');
        const statusAlert = document.getElementById('statusAlert');

        // Tenta iniciar o vídeo assim que carregar
        window.addEventListener('load', () => {
            const playPromise = video.play();

            if (playPromise !== undefined) {
                playPromise.then(_ => {
                    // Autoplay funcionou!
                    overlay.style.opacity = '0';
                    setTimeout(() => overlay.style.display = 'none', 500);
                }).catch(error => {
                    // Autoplay foi bloqueado ou vídeo não encontrado
                    console.log("Autoplay bloqueado ou erro no vídeo");
                });
            }
        });

        function forçarPlay() {
            video.play();
            overlay.style.opacity = '0';
            setTimeout(() => overlay.style.display = 'none', 500);
        }

        function ativarSom() {
            video.muted = false;
            video.volume = 0.7;
        }

        // Se o vídeo der erro (ex: nome do arquivo errado)
        video.onerror = function() {
            statusAlert.classList.remove('hidden');
            console.error("Erro ao carregar o vídeo. Verifique o nome do arquivo.");
        };

        // Remove overlay ao clicar no play do próprio vídeo
        video.onplay = function() {
            overlay.style.opacity = '0';
            setTimeout(() => overlay.style.display = 'none', 500);
        };
    </script>
</body>
</html>


