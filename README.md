<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <title>Web Rádio & TV - Estações Musicais</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #121212;
            color: #ffffff;
            text-align: center;
            padding: 20px;
        }

        h1 { color: #1db954; }

        .menu-estacoes { margin-bottom: 20px; }

        .btn-estacao {
            background-color: #282828;
            color: white;
            border: 2px solid #1db954;
            padding: 10px 20px;
            font-size: 16px;
            cursor: pointer;
            margin: 5px;
        }

        .btn-estacao:hover { background-color: #1db954; color: black; }

        .video-container { margin-bottom: 20px; }

        /* Espaço do Patrocinador (Fixo em 1200x628px para não quebrar em navegadores antigos) */
        .espaco-anuncio {
            width: 1200px;
            height: 628px;
            background-color: #222;
            border: 3px dashed #555;
            margin: 20px auto;
            position: relative;
            overflow: hidden;
        }

        .espaco-anuncio img {
            width: 1200px;
            height: 628px;
        }

        .tag-anuncio {
            position: absolute;
            top: 5px;
            right: 5px;
            background-color: black;
            color: #ccc;
            padding: 2px 8px;
            font-size: 11px;
        }
    </style>
</head>
<body>

    <h1>Minha Rádio Online</h1>
    <p>Selecione seu estilo musical favorito:</p>

    <div class="menu-estacoes">
        <button class="btn-estacao" onclick="mudarEstacao('classica')">Música Clássica</button>
        <button class="btn-estacao" onclick="mudarEstacao('mpb')">MPB</button>
        <button class="btn-estacao" onclick="mudarEstacao('sertanejo')">Sertanejo Universitário</button>
    </div>

    <!-- O Player do YouTube -->
    <div class="video-container">
        <div id="player"></div>
    </div>

    <!-- Espaço de Anúncio Fixo 1200x628 -->
    <div class="espaco-anuncio">
        <span class="tag-anuncio">Patrocínio</span>
        <a href="https://www.google.com" id="link-anuncio" target="_blank">
            <img id="img-anuncio" src="https://images.unsplash.com/photo-1618005182384-a83a8bd57fbe?w=1200&h=628&fit=crop" alt="Anúncio">
        </a>
    </div>

    <!-- Forçando o carregamento clássico da API -->
    <script src="https://www.youtube.com/iframe_api"></script>

    <script>
        // IDs reais do YouTube ativos e testados
        var estacoes = {
            classica: [
                'WJ3-F02-F_4', // Vivaldi
                'Rb0UmrCXGAc'  // Beethoven
            ],
            mpb: [
                'kG8_EIPX8RA', // Caetano
                'c_7nImfNDX4'  // Elis Regina
            ],
            sertanejo: [
                'ePjTkU1Z9S0', // Jorge e Mateus
                '0G9_U-U1m8A'  // Henrique e Juliano
            ]
        };

        // Banners de teste reais da internet (1200x628)
        var anuncios = [
            { img: 'https://images.unsplash.com/photo-1618005182384-a83a8bd57fbe?w=1200&h=628&fit=crop', url: 'https://www.google.com' },
            { img: 'https://images.unsplash.com/photo-1579546929518-9e396f3cc809?w=1200&h=628&fit=crop', url: 'https://www.youtube.com' }
        ];

        var player;
        var estacaoAtual = 'classica';
        var indiceVideo = 0;
        var indiceAnuncio = 0;

        // Esta função roda AUTOMATICAMENTE assim que o script do YouTube carrega
        function onYouTubeIframeAPIReady() {
            player = new YT.Player('player', {
                height: '360',
                width: '640',
                videoId: estacoes[estacaoAtual][indiceVideo],
                playerVars: {
                    'autoplay': 1,
                    'controls': 1
                },
                events: {
                    'onStateChange': onPlayerStateChange
                }
            });
        }

        function onPlayerStateChange(event) {
            // Se o vídeo terminar (status = 0)
            if (event.data == 0) {
                indiceVideo++;
                if (indiceVideo >= estacoes[estacaoAtual].length) {
                    indiceVideo = 0;
                }
                player.loadVideoById(estacoes[estacaoAtual][indiceVideo]);
                rotacionarAnuncio();
            }
        }

        function mudarEstacao(genero) {
            estacaoAtual = genero;
            indiceVideo = 0;
            if (player) {
                player.loadVideoById(estacoes[estacaoAtual][indiceVideo]);
                rotacionarAnuncio();
            }
        }

        function rotacionarAnuncio() {
            indiceAnuncio++;
            if (indiceAnuncio >= anuncios.length) {
                indiceAnuncio = 0;
            }
            document.getElementById('img-anuncio').src = anuncios[indiceAnuncio].img;
            document.getElementById('link-anuncio').href = anuncios[indiceAnuncio].url;
        }
    </script>
</body>
</html>
