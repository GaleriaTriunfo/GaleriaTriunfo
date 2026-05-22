
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Meu AVA - Plataforma de Estudos</title>
    <style>
        :root {
            --primary: #2b6cb0;
            --primary-dark: #1a4373;
            --background: #f7fafc;
            --surface: #ffffff;
            --text: #2d3748;
            --success: #48bb78;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background-color: var(--background);
            color: var(--text);
            display: flex;
            min-height: 100vh;
        }

        /* Barra Lateral */
        nav {
            width: 280px;
            background-color: var(--surface);
            border-right: 1px solid #e2e8f0;
            padding: 20px;
            display: flex;
            flex-direction: column;
        }

        nav h1 {
            font-size: 1.5rem;
            color: var(--primary);
            margin-bottom: 25px;
            text-align: center;
        }

        .progresso-container {
            margin-bottom: 25px;
            background: #edf2f7;
            border-radius: 8px;
            padding: 10px;
        }

        .barra-progresso {
            width: 100%;
            background: #cbd5e0;
            border-radius: 10px;
            overflow: hidden;
            height: 10px;
            margin-top: 5px;
        }

        .progresso-preenchido {
            height: 100%;
            background: var(--success);
            width: 0%;
            transition: width 0.3s ease;
        }

        nav ul {
            list-style: none;
        }

        nav li {
            padding: 12px 15px;
            margin-bottom: 8px;
            border-radius: 6px;
            cursor: pointer;
            transition: all 0.2s;
            font-weight: 500;
        }

        nav li:hover, nav li.ativo {
            background-color: var(--primary);
            color: white;
        }

        /* Conteúdo Principal */
        main {
            flex: 1; /* CORRIGIDO: de flex-1 para flex: 1 */
            width: 100%;
            padding: 40px;
            overflow-y: auto;
        }

        .modulo {
            display: none;
            background: var(--surface);
            padding: 30px;
            border-radius: 8px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.05);
            max-width: 800px;
            animation: fadeIn 0.4s ease;
        }

        .modulo.ativo {
            display: block;
        }

        h2 {
            color: var(--primary-dark);
            margin-bottom: 20px;
        }

        p {
            line-height: 1.6;
            margin-bottom: 15px;
        }

        /* Estilo do Simulado */
        .pergunta {
            margin-bottom: 20px;
            padding: 15px;
            background: #f8fafc;
            border-radius: 6px;
            border-left: 4px solid var(--primary);
        }

        .opcoes label {
            display: block;
            padding: 8px;
            margin: 5px 0;
            background: white;
            border: 1px solid #e2e8f0;
            border-radius: 4px;
            cursor: pointer;
        }

        .opcoes input {
            margin-right: 10px;
        }

        button {
            background-color: var(--primary);
            color: white;
            border: none;
            padding: 12px 24px;
            border-radius: 6px;
            cursor: pointer;
            font-size: 1rem;
            font-weight: bold;
            transition: background 0.2s;
        }

        button:hover {
            background-color: var(--primary-dark);
        }

        .resultado {
            margin-top: 20px;
            padding: 15px;
            font-weight: bold;
            border-radius: 6px;
            display: none;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
    </style>
</head>
<body>

    <!-- Menu Lateral de Navegação -->
    <nav>
        <h1>EduTech AVA</h1>
        
        <div class="progresso-container">
            <span>Seu Progresso: <strong id="porcentagem">0%</strong></span>
            <div class="barra-progresso">
                <div class="progresso-preenchido" id="barra"></div>
            </div>
        </div>

        <ul>
            <li class="item-menu ativo" onclick="mudarModulo('boas-vindas', this)">👋 Boas-vindas</li>
            <li class="item-menu" onclick="mudarModulo('modulo1', this)">📚 Aula 1: Introdução</li>
            <li class="item-menu" onclick="mudarModulo('modulo2', this)">💻 Aula 2: Prática</li>
            <li class="item-menu" onclick="mudarModulo('simulado', this)">📝 Simulado Final</li>
        </ul>
    </nav>

    <!-- Área de Conteúdo -->
    <main>
        <!-- Boas-Vindas -->
        <section id="boas-vindas" class="modulo ativo">
            <h2>Bem-vindo ao seu Ambiente Virtual de Aprendizagem!</h2>
            <p>Este é um protótipo funcional de AVA construído para ser leve, rápido e intuitivo.</p>
            <p><strong>Como navegar:</strong> Utilize o menu lateral esquerdo para alternar entre as aulas. Conforme você avança e responde ao simulado, seu progresso será atualizado.</p>
            <!-- CORRIGIDO: Chamada da função passando o elemento correto do menu para atualizar o foco visual -->
            <button onclick="const el = document.querySelectorAll('.item-menu')[1]; mudarModulo('modulo1', el)">Começar os Estudos</button>
        </section>

        <!-- Módulo 1 -->
        <section id="modulo1" class="modulo">
            <h2>Aula 1: O que é Desenvolvimento Web?</h2>
            <p>O desenvolvimento web refere-se à construção, criação e manutenção de sites. Inclui aspectos como design de web, publicação de web, programação de web e gerenciamento de banco de dados.</p>
            <p>A base da internet é dividida em três pilares principais:</p>
            <ul>
                <li><strong>HTML:</strong> A estrutura e esqueleto da página.</li>
                <li><strong>CSS:</strong> O estilo, cores e posicionamento visual.</li>
                <li><strong>JavaScript:</strong> A lógica e interatividade.</li>
            </ul>
        </section>

        <!-- Módulo 2 -->
        <section id="modulo2" class="modulo">
            <h2>Aula 2: Entendendo o HTML</h2>
            <p>HTML significa <em>HyperText Markup Language</em> (Linguagem de Marcação de Hipertexto). Não é uma linguagem de programação, mas sim uma linguagem de marcação utilizada para informar ao navegador como estruturar o conteúdo.</p>
            <p>Tags fundamentais:</p>
            <pre style="background: #edf2f7; padding: 10px; border-radius: 4px; margin: 10px 0;">
&lt;h1&gt; Para Títulos principais &lt;/h1&gt;
&lt;p&gt; Para parágrafos de texto &lt;/p>
&lt;a href="..."&gt; Para links &lt;/a&gt;
            </pre>
        </section>

        <!-- Simulado -->
        <section id="simulado" class="modulo">
            <h2>Simulado de Avaliação</h2>
            <p>Responda às questões abaixo para testar seus conhecimentos e concluir o curso.</p>
            
            <form id="form-simulado">
                <div class="pergunta">
                    <p><strong>1. O que significa a sigla HTML?</strong></p>
                    <div class="opcoes">
                        <label><input type="radio" name="q1" value="errado"> Hyperlinks and Text Markup Language</label>
                        <label><input type="radio" name="q1" value="correto"> HyperText Markup Language</label>
                        <label><input type="radio" name="q1" value="errado"> Home Tool Markup Language</label>
                    </div>
                </div>

                <div class="pergunta">
                    <p><strong>2. Qual tecnologia é responsável pelo estilo e design visual?</strong></p>
                    <div class="opcoes">
                        <label><input type="radio" name="q2" value="errado"> JavaScript</label>
                        <label><input type="radio" name="q2" value="errado"> HTML</label>
                        <label><input type="radio" name="q2" value="correto"> CSS</label>
                    </div>
                </div>

                <button type="button" onclick="corrigirSimulado()">Enviar Respostas</button>
            </form>

            <div id="resultado-simulado" class="resultado"></div>
        </section>
    </main>

    <!-- Lógica de Interatividade (JavaScript) -->
    <script>
        const paginasVisitadas = new Set(['boas-vindas']);
        const totalPaginas = 4;

        function mudarModulo(idModulo, elementoMenu) {
            document.querySelectorAll('.modulo').forEach(mod => {
                mod.classList.remove('ativo');
            });

            document.querySelectorAll('.item-menu').forEach(item => {
                item.classList.remove('ativo');
            });

            document.getElementById(idModulo).classList.add('ativo');
            if(elementoMenu) elementoMenu.classList.add('ativo');

            paginasVisitadas.add(idModulo);
            atualizarProgresso();
        }

        function atualizarProgresso() {
            const porcentagem = Math.round((paginasVisitadas.size / totalPaginas) * 100);
            document.getElementById('barra').style.width = porcentagem + '%';
            document.getElementById('porcentagem').innerText = porcentagem + '%';
        }

        function corrigirSimulado() {
            const form = document.getElementById('form-simulado');
            const respostas = new FormData(form);
            
            let nota = 0;
            let totalQuestoes = 2;

            for (let value of respostas.values()) {
                if (value === 'correto') {
                    nota++;
                }
            }

            const resultadoDiv = document.getElementById('resultado-simulado');
            resultadoDiv.style.display = 'block';

            if (nota === totalQuestoes) {
                resultadoDiv.style.backgroundColor = '#c6f6d5';
                resultadoDiv.style.color = '#22543d';
                resultadoDiv.innerHTML = `🎉 Excelente! Você acertou ${nota} de ${totalQuestoes}. Curso Concluído!`;
            } else {
                resultadoDiv.style.backgroundColor = '#fed7d7';
                resultadoDiv.style.color = '#742a2a';
                resultadoDiv.innerHTML = `🏃 Quase lá! Você acertou ${nota} de ${totalQuestoes}. Revise o conteúdo e tente novamente.`;
            }
        }
    </script>
</body>
</html>
