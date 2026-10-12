
<html lang="pt-BR" class="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>O Computador Supremo - Matriz de Dados Interestelar</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        space: {
                            950: '#020617',
                            900: '#030712',
                            800: '#0b0f19',
                            700: '#111827',
                        },
                        matrix: {
                            cyan: '#00f3ff',
                            emerald: '#10b981',
                            violet: '#a855f7',
                            amber: '#f59e0b',
                            rose: '#f43f5e'
                        }
                    },
                    fontFamily: {
                        mono: ['JetBrains Mono', 'Courier New', monospace],
                        orbitron: ['Orbitron', 'sans-serif']
                    }
                }
            }
        }
    </script>
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;700&family=Orbitron:wght@500;700;900&display=swap" rel="stylesheet">
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        body {
            font-family: 'JetBrains Mono', monospace;
            background-color: #020617;
            color: #f8fafc;
            overflow-x: hidden;
        }
        h1, h2, h3, .font-orbitron {
            font-family: 'Orbitron', sans-serif;
        }
        .glow-cyan {
            box-shadow: 0 0 25px rgba(0, 243, 255, 0.35);
        }
        .glow-violet {
            box-shadow: 0 0 25px rgba(168, 85, 247, 0.4);
        }
        .glow-emerald {
            box-shadow: 0 0 25px rgba(16, 185, 129, 0.35);
        }
        .text-glow-cyan {
            text-shadow: 0 0 12px rgba(0, 243, 255, 0.8);
        }
        .text-glow-violet {
            text-shadow: 0 0 12px rgba(168, 85, 247, 0.8);
        }
        .scanline {
            background: linear-gradient(
                to bottom,
                rgba(255,255,255,0),
                rgba(255,255,255,0) 50%,
                rgba(0, 243, 255, 0.02) 50%,
                rgba(0, 243, 255, 0.02)
            );
            background-size: 100% 4px;
        }
        ::-webkit-scrollbar {
            width: 6px;
        }
        ::-webkit-scrollbar-track {
            background: #030712;
        }
        ::-webkit-scrollbar-thumb {
            background: #111827;
            border-radius: 3px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #00f3ff;
        }
    </style>
</head>
<body class="min-h-screen flex flex-col bg-space-950 scanline">

    <!-- Header / Navigation Bar -->
    <header class="border-b border-matrix-cyan/30 bg-space-900/90 backdrop-blur-md sticky top-0 z-50 px-4 py-3">
        <div class="max-w-7xl mx-auto flex flex-col md:flex-row items-center justify-between gap-4">
            
            <div class="flex items-center space-x-3">
                <div class="w-10 h-10 rounded-xl bg-space-800 border border-matrix-cyan flex items-center justify-center glow-cyan transition-all">
                    <i class="fa-solid fa-network-wired text-matrix-cyan text-xl"></i>
                </div>
                <div>
                    <h1 class="text-xl font-black tracking-wider text-matrix-cyan text-glow-cyan">S.R.O.S. // SUPREME COMPUTER</h1>
                    <p class="text-[10px] text-slate-400 uppercase tracking-widest">Matriz de Dados Interestelar</p>
                </div>
            </div>

            <!-- Simulation Mode Selector Tabs -->
            <div class="flex flex-wrap items-center gap-1.5 bg-space-950/80 p-1.5 rounded-xl border border-space-800">
                <button onclick="setSimulationMode('idle')" id="tab-idle" class="px-3.5 py-1.5 rounded-lg text-xs font-bold transition-all bg-matrix-cyan/25 text-matrix-cyan border border-matrix-cyan/60 glow-cyan flex items-center gap-2">
                    <i class="fa-solid fa-satellite"></i> Repouso / Malha Base
                </button>
                <button onclick="setSimulationMode('climate')" id="tab-climate" class="px-3.5 py-1.5 rounded-lg text-xs font-bold transition-all text-slate-400 hover:text-matrix-cyan hover:bg-space-800 border border-transparent flex items-center gap-2">
                    <i class="fa-solid fa-globe"></i> Simulação Climática Global
                </button>
                <button onclick="setSimulationMode('universe')" id="tab-universe" class="px-3.5 py-1.5 rounded-lg text-xs font-bold transition-all text-slate-400 hover:text-matrix-violet hover:bg-space-800 border border-transparent flex items-center gap-2">
                    <i class="fa-solid fa-atom"></i> Evolução do Universo
                </button>
            </div>

            <!-- Top Actions -->
            <div class="flex items-center space-x-3">
                <button onclick="toggleAudio()" id="btn-audio" class="w-9 h-9 rounded-xl bg-space-800 border border-space-700 hover:border-matrix-cyan text-slate-300 flex items-center justify-center text-xs transition-all" title="Alternar Som Sintetizador">
                    <i class="fa-solid fa-volume-xmark" id="audio-icon"></i>
                </button>
                <button onclick="openModal()" class="px-3 py-1.5 rounded-xl bg-space-800 border border-matrix-cyan/40 hover:border-matrix-cyan text-matrix-cyan text-xs font-bold flex items-center gap-2 transition-all glow-cyan">
                    <i class="fa-solid fa-book-open"></i> Visão Geral do Aplicativo
                </button>
            </div>
        </div>
    </header>

    <!-- Main Content Grid -->
    <main class="flex-1 max-w-7xl w-full mx-auto p-4 grid grid-cols-1 lg:grid-cols-4 gap-4">
        
        <!-- Canvas Simulation Area (3 Cols) -->
        <div class="lg:col-span-3 flex flex-col gap-4">
            
            <div id="canvas-wrapper" class="relative w-full aspect-[16/10] bg-space-900 rounded-2xl border border-matrix-cyan/30 overflow-hidden glow-cyan flex items-center justify-center transition-all">
                
                <!-- Main Canvas Element -->
                <canvas id="simCanvas" class="w-full h-full block cursor-crosshair"></canvas>

                <!-- Floating HUD Overlays -->
                <div class="absolute top-4 left-4 bg-space-950/85 backdrop-blur-md p-3 rounded-xl border border-matrix-cyan/30 text-xs space-y-1 pointer-events-none">
                    <div id="hud-sim-title" class="text-matrix-cyan font-bold uppercase tracking-wider flex items-center gap-2">
                        <i class="fa-solid fa-circle-nodes animate-pulse"></i> <span>MODO: MALHA INTERESTELAR EM REPOUSO</span>
                    </div>
                    <div class="text-slate-400">FPS: <span id="hud-fps" class="text-white">60</span> | LATÊNCIA CAUSAL: <span id="hud-latency" class="text-emerald-400">0.0002 ms</span></div>
                    <div class="text-slate-400">NÓS DA FROTA ATIVOS: <span id="hud-nodes" class="text-matrix-cyan">18</span> / 18</div>
                </div>

                <!-- Simulation Playback Controls Bar -->
                <div class="absolute bottom-4 left-1/2 -translate-x-1/2 bg-space-950/90 backdrop-blur-md px-6 py-3 rounded-2xl border border-matrix-cyan/40 flex items-center gap-4 shadow-2xl">
                    <button onclick="togglePlayPause()" id="btn-play" class="w-10 h-10 rounded-xl bg-matrix-cyan hover:bg-emerald-400 text-space-950 font-bold flex items-center justify-center transition-all glow-cyan">
                        <i class="fa-solid fa-pause" id="icon-play"></i>
                    </button>
                    <div class="h-6 w-[1px] bg-space-800"></div>
                    <div class="flex items-center gap-2">
                        <span class="text-xs text-slate-400 uppercase">Velocidade:</span>
                        <button onclick="setSpeed(1)" id="spd-1" class="px-2.5 py-1 rounded-lg text-xs font-bold bg-matrix-cyan/25 text-matrix-cyan border border-matrix-cyan">1x</button>
                        <button onclick="setSpeed(3)" id="spd-3" class="px-2.5 py-1 rounded-lg text-xs font-bold bg-space-800 text-slate-400 border border-space-700">3x</button>
                        <button onclick="setSpeed(5)" id="spd-5" class="px-2.5 py-1 rounded-lg text-xs font-bold bg-space-800 text-slate-400 border border-space-700">5x</button>
                    </div>
                    <div class="h-6 w-[1px] bg-space-800"></div>
                    <button onclick="triggerQuantumSync()" class="px-3.5 py-2 rounded-xl bg-violet-950/80 hover:bg-violet-900 text-xs text-violet-300 border border-violet-500/50 flex items-center gap-2 transition-all font-bold glow-violet">
                        <i class="fa-solid fa-atom animate-spin"></i> Sincronização Quântica HD
                    </button>
                </div>
            </div>

            <!-- Description Box -->
            <div class="bg-space-900/90 backdrop-blur-md p-4 rounded-2xl border border-space-800 text-sm">
                <h3 class="font-bold text-matrix-cyan mb-1 flex items-center gap-2"><i class="fa-solid fa-circle-info"></i> Arquitetura de Processamento Descentralizado</h3>
                <p id="view-desc" class="text-slate-300 text-xs leading-relaxed">
                    O SROS une a frota de naves em uma supercomputação distribuída via laser Full Duplex e relógios de emaranhamento quântico. A latência causal é zerada, permitindo simulações planetárias e cosmológicas massivas sem perda de informações.
                </p>
            </div>

        </div>

        <!-- Sidebar (Telemetry & Controls) -->
        <div class="lg:col-span-1 flex flex-col gap-4">
            
            <!-- Telemetry Panel -->
            <div class="bg-space-900/90 backdrop-blur-md p-4 rounded-2xl border border-matrix-cyan/30 flex flex-col gap-4">
                <div class="flex items-center justify-between border-b border-space-800 pb-3">
                    <h2 class="font-orbitron font-bold text-sm text-matrix-cyan flex items-center gap-2">
                        <i class="fa-solid fa-chart-line"></i> Telemetria Global
                    </h2>
                    <span id="system-status-badge" class="text-[10px] bg-emerald-500/20 text-emerald-400 px-2 py-0.5 rounded border border-emerald-500/40">SINCRO OK</span>
                </div>

                <!-- Metrics -->
                <div class="space-y-3 text-xs">
                    <div>
                        <div class="flex justify-between mb-1">
                            <span class="text-slate-400">Poder Global (YottaFLOPS)</span>
                            <span id="val-yotta" class="text-matrix-cyan font-bold">14.8 YFLOPS</span>
                        </div>
                        <div class="w-full bg-space-950 rounded-full h-2 overflow-hidden border border-space-800">
                            <div id="bar-yotta" class="bg-matrix-cyan h-full transition-all duration-300" style="width: 74%;"></div>
                        </div>
                    </div>

                    <div>
                        <div class="flex justify-between mb-1">
                            <span class="text-slate-400">Coerência Quântica</span>
                            <span id="val-coherence" class="text-violet-400 font-bold">99.987%</span>
                        </div>
                        <div class="w-full bg-space-950 rounded-full h-2 overflow-hidden border border-space-800">
                            <div id="bar-coherence" class="bg-violet-500 h-full transition-all duration-300" style="width: 99.98%;"></div>
                        </div>
                    </div>

                    <div>
                        <div class="flex justify-between mb-1">
                            <span class="text-slate-400">Carga da Simulação Atual</span>
                            <span id="val-load" class="text-amber-400 font-bold">42.5%</span>
                        </div>
                        <div class="w-full bg-space-950 rounded-full h-2 overflow-hidden border border-space-800">
                            <div id="bar-load" class="bg-amber-400 h-full transition-all duration-300" style="width: 42.5%;"></div>
                        </div>
                    </div>
                </div>

                <!-- Controls -->
                <div class="space-y-3 pt-2 border-t border-space-800">
                    <h3 class="font-bold text-xs text-matrix-cyan uppercase">Parâmetros da Rede</h3>

                    <div class="space-y-1">
                        <div class="flex justify-between text-xs">
                            <span class="text-slate-400">Freq. Emaranhamento Quântico</span>
                            <span id="label-freq" class="text-violet-400 font-bold">4.8 THz</span>
                        </div>
                        <input type="range" id="freqSlider" min="1.0" max="10.0" step="0.1" value="4.8" 
                            class="w-full accent-violet-400 bg-space-950 rounded-lg appearance-none cursor-pointer h-2 border border-space-800"
                            oninput="updateQuantumFreq(this.value)">
                    </div>

                    <div class="space-y-1">
                        <div class="flex justify-between text-xs">
                            <span class="text-slate-400">Potência Rede Lasers Full Duplex</span>
                            <span id="label-laser" class="text-matrix-cyan font-bold">85%</span>
                        </div>
                        <input type="range" id="laserSlider" min="20" max="100" step="5" value="85" 
                            class="w-full accent-matrix-cyan bg-space-950 rounded-lg appearance-none cursor-pointer h-2 border border-space-800"
                            oninput="updateLaserPower(this.value)">
                    </div>
                </div>

            </div>

            <!-- Terminal Log -->
            <div class="bg-space-900/90 backdrop-blur-md p-4 rounded-2xl border border-space-800 flex flex-col flex-1 min-h-[180px]">
                <div class="flex items-center justify-between border-b border-space-800 pb-2 mb-2">
                    <h3 class="font-orbitron font-bold text-xs text-matrix-cyan flex items-center gap-2">
                        <i class="fa-solid fa-terminal"></i> Log da Matriz SROS
                    </h3>
                    <button onclick="clearLogs()" class="text-[10px] text-slate-400 hover:text-matrix-cyan underline">Limpar</button>
                </div>
                <div id="log-container" class="flex-1 overflow-y-auto space-y-1.5 font-mono text-[11px] text-slate-300 max-h-[160px]">
                    <div class="text-matrix-cyan">[08:34:00] SROS Matriz Interestelar inicializada.</div>
                    <div class="text-violet-400">[08:34:01] 18 relógios quânticos sincronizados em malha estelar.</div>
                    <div class="text-emerald-400">[08:34:02] Latência causal reduzida a 0.0002 ms via IA AutoNav.</div>
                </div>
            </div>

        </div>

    </main>

    <!-- Node Inspection Modal / Card -->
    <div id="nodeModal" class="fixed inset-0 bg-space-950/80 backdrop-blur-sm z-50 flex items-center justify-center p-4 hidden">
        <div class="bg-space-900 border border-matrix-cyan/50 rounded-2xl max-w-lg w-full p-6 space-y-4 glow-cyan relative">
            <div class="flex items-center justify-between border-b border-space-800 pb-3">
                <h3 id="modal-node-title" class="font-orbitron font-bold text-base text-matrix-cyan flex items-center gap-2">
                    <i class="fa-solid fa-satellite-dish"></i> Inspeção de Nó: SROS-Alpha-01
                </h3>
                <button onclick="closeNodeModal()" class="text-slate-400 hover:text-white text-lg"><i class="fa-solid fa-xmark"></i></button>
            </div>
            
            <div class="space-y-3 text-xs text-slate-300">
                <div class="grid grid-cols-2 gap-3 bg-space-950 p-3 rounded-xl border border-space-800">
                    <div>
                        <span class="text-slate-400 block">Classe da Nave:</span>
                        <span id="modal-node-class" class="text-white font-bold">Cruzador de Pesquisa</span>
                    </div>
                    <div>
                        <span class="text-slate-400 block">IA AutoNav:</span>
                        <span id="modal-node-autonav" class="text-emerald-400 font-bold">Ativa (Nível 9)</span>
                    </div>
                    <div>
                        <span class="text-slate-400 block">Carga de Processamento:</span>
                        <span id="modal-node-cpu" class="text-matrix-cyan font-bold">78.4%</span>
                    </div>
                    <div>
                        <span class="text-slate-400 block">Conexões Laser:</span>
                        <span id="modal-node-links" class="text-violet-400 font-bold">4 Links Ativos</span>
                    </div>
                </div>

                <p class="text-slate-400 leading-relaxed">
                    Este nó processa sub-rotinas locais da simulação atual utilizando algoritmos preditivos de IA AutoNav e transmite resultados delta instantaneamente via feixes Full Duplex.
                </p>
            </div>

            <div class="pt-3 border-t border-space-800 flex justify-end">
                <button onclick="closeNodeModal()" class="px-4 py-2 rounded-xl bg-matrix-cyan text-space-950 font-bold text-xs hover:bg-emerald-400 transition-all glow-cyan">
                    Fechar Inspeção
                </button>
            </div>
        </div>
    </div>

    <!-- Application Overview Modal -->
    <div id="infoModal" class="fixed inset-0 bg-space-950/80 backdrop-blur-sm z-50 flex items-center justify-center p-4 hidden">
        <div class="bg-space-900 border border-matrix-cyan/50 rounded-2xl max-w-2xl w-full p-6 space-y-4 glow-cyan relative max-h-[90vh] overflow-y-auto">
            <div class="flex items-center justify-between border-b border-space-800 pb-3">
                <h3 class="font-orbitron font-bold text-lg text-matrix-cyan flex items-center gap-2">
                    <i class="fa-solid fa-network-wired text-matrix-cyan"></i> Visão Geral & Fundamentos do SROS
                </h3>
                <button onclick="closeModal()" class="text-slate-400 hover:text-white text-lg"><i class="fa-solid fa-xmark"></i></button>
            </div>
            
            <div class="space-y-3 text-xs text-slate-300 leading-relaxed">
                <p>
                    <strong class="text-matrix-cyan">Problema Resolvido:</strong> O limite astronômico de processamento de dados e a perda severa de informações em simulações complexas em larga escala, como a previsão climática global de exoplanetas ou o rastreamento da evolução do universo.
                </p>
                <p>
                    <strong class="text-violet-400">Lasers Full Duplex & Emaranhamento:</strong> A rede de lasers Full Duplex do SROS combinada com relógios de emaranhamento quântico transforma a frota de naves espalhadas pela galáxia em um único supercomputador descentralizado.
                </p>
                <p>
                    <strong class="text-emerald-400">Mitigação de Latência Causal:</strong> A latência inerente às distâncias interestelares é neutralizada porque os dados são processados localmente pelas instâncias de IA AutoNav em cada nave e sincronizados instantaneamente por flutuações quânticas.
                </p>
                <div class="bg-space-950 p-3 rounded-xl border border-space-800 space-y-1">
                    <div class="font-bold text-matrix-cyan">Recursos do Simulador:</div>
                    <ul class="list-disc pl-4 space-y-1 text-slate-400">
                        <li><strong>Mapa Galáctico 2D:</strong> Visualização em tempo real de nós da frota interconectados por feixes de laser luminescentes.</li>
                        <li><strong>Simulações Ativas:</strong> Alterne entre Simulação Climática Global e Evolução do Universo com telemetria dinâmica em YottaFLOPS.</li>
                        <li><strong>Inspeção de Nós:</strong> Clique em qualquer nave no canvas para inspecionar o status de sua IA AutoNav e carga de processamento.</li>
                    </ul>
                </div>
            </div>

            <div class="pt-3 border-t border-space-800 flex justify-end">
                <button onclick="closeModal()" class="px-4 py-2 rounded-xl bg-matrix-cyan text-space-950 font-bold text-xs hover:bg-emerald-400 transition-all glow-cyan">
                    Entendido, Iniciar Matriz
                </button>
            </div>
        </div>
    </div>

    <script>
        const canvas = document.getElementById('simCanvas');
        const ctx = canvas.getContext('2d');

        let simulationMode = 'idle'; // 'idle', 'climate', 'universe'
        let isRunning = true;
        let timeScale = 1;
        let simulationTime = 0;
        
        let quantumFreq = 4.8;
        let laserPower = 85;
        let globalYotta = 14.8;
        let coherence = 99.987;
        let simLoad = 42.5;

        let quantumPulses = []; // Expanding rings from sync button

        // Fleet Nodes Initialization
        let nodes = [
            { id: 1, name: "SROS-Alpha-01", class: "Cruzador Pesado", x: 150, y: 120, vx: 0.2, vy: -0.1, cpu: 82.4, links: [2, 3, 4], autonav: "Ativa (Nv.9)" },
            { id: 2, name: "SROS-Beta-04", class: "Nave Científica", x: 350, y: 90, vx: -0.1, vy: 0.15, cpu: 65.1, links: [1, 5, 6], autonav: "Ativa (Nv.9)" },
            { id: 3, name: "SROS-Gamma-09", class: "Sonda de Deep Space", x: 220, y: 280, vx: 0.15, vy: 0.1, cpu: 91.2, links: [1, 7], autonav: "Ativa (Nv.8)" },
            { id: 4, name: "SROS-Delta-12", class: "Cruzador Pesado", x: 480, y: 220, vx: -0.2, vy: -0.1, cpu: 74.5, links: [1, 2, 8], autonav: "Ativa (Nv.9)" },
            { id: 5, name: "SROS-Epsilon-02", class: "Estação Orbital", x: 650, y: 110, vx: 0.05, vy: 0.05, cpu: 88.9, links: [2, 6, 9], autonav: "Ativa (Nv.10)" },
            { id: 6, name: "SROS-Zeta-05", class: "Nave de Reparo", x: 580, y: 320, vx: -0.1, vy: -0.15, cpu: 55.0, links: [2, 5, 10], autonav: "Ativa (Nv.8)" },
            { id: 7, name: "SROS-Theta-08", class: "Sonda Quântica", x: 100, y: 410, vx: 0.1, vy: -0.2, cpu: 94.3, links: [3, 11], autonav: "Ativa (Nv.9)" },
            { id: 8, name: "SROS-Iota-03", class: "Cruzador Pesado", x: 750, y: 240, vx: -0.15, vy: 0.1, cpu: 79.8, links: [4, 5, 12], autonav: "Ativa (Nv.9)" },
            { id: 9, name: "SROS-Kappa-11", class: "Nave Científica", x: 880, y: 130, vx: 0.05, vy: -0.1, cpu: 81.2, links: [5, 8], autonav: "Ativa (Nv.9)" },
            { id: 10, name: "SROS-Lambda-06", class: "Sonda de Deep Space", x: 720, y: 430, vx: 0.1, vy: 0.1, cpu: 62.4, links: [6, 8, 13], autonav: "Ativa (Nv.8)" },
            { id: 11, name: "SROS-Mu-07", class: "Estação Orbital", x: 280, y: 470, vx: -0.05, vy: -0.05, cpu: 70.1, links: [3, 7, 14], autonav: "Ativa (Nv.10)" },
            { id: 12, name: "SROS-Nu-14", class: "Nave Científica", x: 950, y: 380, vx: -0.1, vy: -0.1, cpu: 85.6, links: [8, 9, 15], autonav: "Ativa (Nv.9)" },
            { id: 13, name: "SROS-Xi-10", class: "Cruzador Pesado", x: 500, y: 480, vx: 0.15, vy: -0.05, cpu: 89.0, links: [6, 10, 11], autonav: "Ativa (Nv.9)" },
            { id: 14, name: "SROS-Omicron-13", class: "Sonda Quântica", x: 400, y: 360, vx: -0.1, vy: 0.1, cpu: 77.3, links: [3, 4, 13], autonav: "Ativa (Nv.9)" },
            { id: 15, name: "SROS-Pi-15", class: "Estação Orbital", x: 820, y: 500, vx: 0.05, vy: -0.1, cpu: 92.1, links: [10, 12, 14], autonav: "Ativa (Nv.10)" }
        ];

        let selectedNode = null;

        function resizeCanvas() {
            const rect = canvas.getBoundingClientRect();
            canvas.width = rect.width * window.devicePixelRatio;
            canvas.height = rect.height * window.devicePixelRatio;
            ctx.scale(window.devicePixelRatio, window.devicePixelRatio);
        }
        window.addEventListener('resize', resizeCanvas);
        resizeCanvas();

        // --- AUDIO SYSTEM (Web Audio API Synth) ---
        let audioCtx = null;
        let audioMuted = true;
        let ambientOsc = null;
        let ambientGain = null;

        function toggleAudio() {
            audioMuted = !audioMuted;
            const icon = document.getElementById('audio-icon');
            if (!audioMuted) {
                icon.className = "fa-solid fa-volume-high text-matrix-cyan";
                initWebAudio();
                addLog("Áudio sintetizador da matriz ativado.");
            } else {
                icon.className = "fa-solid fa-volume-xmark";
                if (audioCtx && audioCtx.state === 'running') {
                    audioCtx.suspend();
                }
                addLog("Áudio desativado.");
            }
        }

        function initWebAudio() {
            if (!audioCtx) {
                audioCtx = new (window.AudioContext || window.webkitAudioContext)();
            }
            if (audioCtx.state === 'suspended') {
                audioCtx.resume();
            }
            if (!ambientOsc) {
                ambientOsc = audioCtx.createOscillator();
                ambientGain = audioCtx.createGain();
                
                ambientOsc.type = 'sawtooth';
                ambientOsc.frequency.setValueAtTime(65, audioCtx.currentTime);
                ambientGain.gain.setValueAtTime(0.015, audioCtx.currentTime);

                ambientOsc.connect(ambientGain);
                ambientGain.connect(audioCtx.destination);
                ambientOsc.start();
            }
        }

        // --- INTERACTION / CLICKS ---
        canvas.addEventListener('click', (e) => {
            const rect = canvas.getBoundingClientRect();
            const mouseX = e.clientX - rect.left;
            const mouseY = e.clientY - rect.top;

            // Scale to CSS coordinate space
            for (let node of nodes) {
                let dx = node.x - mouseX;
                let dy = node.y - mouseY;
                let dist = Math.sqrt(dx * dx + dy * dy);
                if (dist < 20) {
                    inspectNode(node);
                    break;
                }
            }
        });

        function inspectNode(node) {
            selectedNode = node;
            document.getElementById('modal-node-title').innerHTML = `<i class="fa-solid fa-satellite-dish"></i> Inspeção de Nó: ${node.name}`;
            document.getElementById('modal-node-class').innerText = node.class;
            document.getElementById('modal-node-autonav').innerText = node.autonav;
            document.getElementById('modal-node-cpu').innerText = node.cpu.toFixed(1) + "%";
            document.getElementById('modal-node-links').innerText = node.links.length + " Links Ativos";
            document.getElementById('nodeModal').classList.remove('hidden');
            addLog(`Inspecionando nó da frota: ${node.name} (${node.class}).`);
        }

        function closeNodeModal() {
            document.getElementById('nodeModal').classList.add('hidden');
        }

        // --- SIMULATION MODE SWITCHING ---
        function setSimulationMode(mode) {
            simulationMode = mode;
            ['idle', 'climate', 'universe'].forEach(m => {
                const btn = document.getElementById(`tab-${m}`);
                if (m === mode) {
                    if (m === 'universe') {
                        btn.className = "px-3.5 py-1.5 rounded-lg text-xs font-bold transition-all bg-matrix-violet/25 text-matrix-violet border border-matrix-violet/60 glow-violet flex items-center gap-2";
                    } else if (m === 'climate') {
                        btn.className = "px-3.5 py-1.5 rounded-lg text-xs font-bold transition-all bg-matrix-cyan/25 text-matrix-cyan border border-matrix-cyan/60 glow-cyan flex items-center gap-2";
                    } else {
                        btn.className = "px-3.5 py-1.5 rounded-lg text-xs font-bold transition-all bg-matrix-cyan/25 text-matrix-cyan border border-matrix-cyan/60 glow-cyan flex items-center gap-2";
                    }
                } else {
                    btn.className = "px-3.5 py-1.5 rounded-lg text-xs font-bold transition-all text-slate-400 hover:text-matrix-cyan hover:bg-space-800 border border-transparent flex items-center gap-2";
                }
            });

            const titles = {
                idle: "MODO: MALHA INTERESTELAR EM REPOUSO",
                climate: "MODO: SIMULAÇÃO CLIMÁTICA GLOBAL EM ANDAMENTO",
                universe: "MODO: SIMULAÇÃO COSMOLÓGICA (BIG BANG AO T+15B)"
            };
            const descs = {
                idle: "O SROS mantém a rede sincronizada com feixes laser de baixa largura de banda e relógios quânticos em espera.",
                climate: "Processando 500 bilhões de variáveis atmosféricas planetárias em paralelo via feixes Full Duplex.",
                universe: "Simulando a evolução de matéria escura, aglomerados de galáxias e expansão estelar em tempo real com coerência quântica 99.99%."
            };

            document.getElementById('hud-sim-title').querySelector('span').innerText = titles[mode];
            document.getElementById('view-desc').innerText = descs[mode];

            if (mode === 'idle') {
                globalYotta = 14.8;
                simLoad = 42.5;
            } else if (mode === 'climate') {
                globalYotta = 84.5;
                simLoad = 88.2;
            } else if (mode === 'universe') {
                globalYotta = 245.0;
                simLoad = 99.4;
            }

            document.getElementById('val-yotta').innerText = globalYotta.toFixed(1) + " YFLOPS";
            document.getElementById('bar-yotta').style.width = Math.min(100, (globalYotta / 250) * 100) + "%";
            document.getElementById('val-load').innerText = simLoad.toFixed(1) + "%";
            document.getElementById('bar-load').style.width = simLoad + "%";

            addLog(`Alternado para o modo de simulação: ${mode.toUpperCase()}`);
        }

        // --- CONTROLS ---
        function togglePlayPause() {
            isRunning = !isRunning;
            const icon = document.getElementById('icon-play');
            const btn = document.getElementById('btn-play');
            if (isRunning) {
                icon.className = "fa-solid fa-pause";
                btn.classList.add('bg-matrix-cyan', 'glow-cyan');
                btn.classList.remove('bg-space-800');
                addLog("Simulação retomada.");
            } else {
                icon.className = "fa-solid fa-play";
                btn.classList.remove('bg-matrix-cyan', 'glow-cyan');
                btn.classList.add('bg-space-800');
                addLog("Simulação pausada.");
            }
        }

        function setSpeed(spd) {
            timeScale = spd;
            [1, 3, 5].forEach(s => {
                const b = document.getElementById(`spd-${s}`);
                if (s === spd) {
                    b.className = "px-2.5 py-1 rounded-lg text-xs font-bold bg-matrix-cyan/25 text-matrix-cyan border border-matrix-cyan";
                } else {
                    b.className = "px-2.5 py-1 rounded-lg text-xs font-bold bg-space-800 text-slate-400 border border-space-700";
                }
            });
            addLog(`Velocidade da matriz ajustada para ${spd}x.`);
        }

        function updateQuantumFreq(val) {
            quantumFreq = parseFloat(val);
            document.getElementById('label-freq').innerText = quantumFreq.toFixed(1) + " THz";
            coherence = Math.min(99.999, 99.900 + (quantumFreq * 0.01));
            document.getElementById('val-coherence').innerText = coherence.toFixed(3) + "%";
            document.getElementById('bar-coherence').style.width = coherence + "%";
            addLog(`Frequência de Emaranhamento Quântico ajustada para ${quantumFreq.toFixed(1)} THz.`);
        }

        function updateLaserPower(val) {
            laserPower = parseInt(val);
            document.getElementById('label-laser').innerText = laserPower + "%";
            addLog(`Potência da Rede de Lasers Full Duplex ajustada para ${laserPower}%.`);
        }

        function triggerQuantumSync() {
            quantumPulses.push({ x: canvas.width / (2 * window.devicePixelRatio), y: canvas.height / (2 * window.devicePixelRatio), r: 10, maxR: 600, alpha: 1.0 });
            coherence = 99.999;
            document.getElementById('val-coherence').innerText = "99.999%";
            document.getElementById('bar-coherence').style.width = "100%";
            addLog("Sincronização Quântica de Alta Densidade disparada! Coerência máxima atingida.");
        }

        function openModal() {
            document.getElementById('infoModal').classList.remove('hidden');
        }
        function closeModal() {
            document.getElementById('infoModal').classList.add('hidden');
        }

        function clearLogs() {
            document.getElementById('log-container').innerHTML = `<div class="text-slate-400">[Console limpo pelo operador]</div>`;
        }

        function addLog(text) {
            const container = document.getElementById('log-container');
            const now = new Date().toTimeString().split(' ')[0];
            const div = document.createElement('div');
            div.className = "text-slate-300";
            div.innerHTML = `<span class="text-matrix-cyan">[${now}]</span> ${text}`;
            container.appendChild(div);
            container.scrollTop = container.scrollHeight;
        }

        // --- DRAWING FUNCTIONS ---

        function drawStarfield(w, h) {
            ctx.fillStyle = '#020617';
            ctx.fillRect(0, 0, w, h);

            // Subtle nebula clouds
            const nebGrad = ctx.createRadialGradient(w * 0.3, h * 0.3, 50, w * 0.3, h * 0.3, w * 0.6);
            nebGrad.addColorStop(0, 'rgba(0, 243, 255, 0.04)');
            nebGrad.addColorStop(0.5, 'rgba(168, 85, 247, 0.02)');
            nebGrad.addColorStop(1, 'transparent');
            ctx.fillStyle = nebGrad;
            ctx.fillRect(0, 0, w, h);

            // Stars
            ctx.fillStyle = '#ffffff';
            for (let i = 0; i < 80; i++) {
                let x = (Math.sin(i * 123) * 10000) % w;
                let y = (Math.cos(i * 456) * 10000) % h;
                if (x < 0) x += w;
                if (y < 0) y += h;
                let alpha = 0.2 + (Math.sin(simulationTime * 0.03 + i) * 0.2);
                ctx.globalAlpha = Math.max(0.1, alpha);
                ctx.fillRect(x, y, 1.5, 1.5);
            }
            ctx.globalAlpha = 1.0;
        }

        function drawGalacticMap(w, h) {
            drawStarfield(w, h);

            // Move nodes slightly based on velocity
            if (isRunning) {
                for (let node of nodes) {
                    node.x += node.vx * timeScale * 0.2;
                    node.y += node.vy * timeScale * 0.2;

                    // Bounce off boundaries
                    if (node.x < 50 || node.x > w - 50) node.vx *= -1;
                    if (node.y < 50 || node.y > h - 50) node.vy *= -1;
                }
            }

            // Draw Quantum Entanglement Waves (Concentric expanding rings)
            for (let i = quantumPulses.length - 1; i >= 0; i--) {
                let p = quantumPulses[i];
                if (isRunning) {
                    p.r += 6 * timeScale;
                    p.alpha -= 0.015 * timeScale;
                }
                if (p.alpha <= 0 || p.r > p.maxR) {
                    quantumPulses.splice(i, 1);
                    continue;
                }
                ctx.strokeStyle = `rgba(168, 85, 247, ${p.alpha})`;
                ctx.lineWidth = 2;
                ctx.beginPath();
                ctx.arc(p.x, p.y, p.r, 0, Math.PI * 2);
                ctx.stroke();
            }

            // Draw Full Duplex Laser Connections between nodes
            for (let node of nodes) {
                for (let targetId of node.links) {
                    let target = nodes.find(n => n.id === targetId);
                    if (target) {
                        // Laser line
                        ctx.strokeStyle = simulationMode === 'universe' ? 'rgba(168, 85, 247, 0.35)' : 'rgba(0, 243, 255, 0.25)';
                        ctx.lineWidth = 1.5;
                        ctx.beginPath();
                        ctx.moveTo(node.x, node.y);
                        ctx.lineTo(target.x, target.y);
                        ctx.stroke();

                        // Data stream pulses traveling both ways (Full Duplex)
                        if (isRunning) {
                            let t1 = ((simulationTime * 0.04) % 1);
                            let t2 = (((simulationTime * 0.04) + 0.5) % 1);
                            
                            let px1 = node.x + (target.x - node.x) * t1;
                            let py1 = node.y + (target.y - node.y) * t1;

                            let px2 = target.x + (node.x - target.x) * t2;
                            let py2 = target.y + (node.y - target.y) * t2;

                            ctx.fillStyle = '#ffffff';
                            ctx.beginPath();
                            ctx.arc(px1, py1, 2.5, 0, Math.PI * 2);
                            ctx.arc(px2, py2, 2.5, 0, Math.PI * 2);
                            ctx.fill();
                        }
                    }
                }
            }

            // Draw Fleet Nodes
            for (let node of nodes) {
                // Outer glow
                let glowColor = simulationMode === 'universe' ? 'rgba(168, 85, 247, 0.5)' : 'rgba(0, 243, 255, 0.5)';
                ctx.fillStyle = glowColor;
                ctx.beginPath();
                ctx.arc(node.x, node.y, 14, 0, Math.PI * 2);
                ctx.fill();

                // Core Node Circle
                ctx.fillStyle = '#030712';
                ctx.strokeStyle = simulationMode === 'universe' ? '#a855f7' : '#00f3ff';
                ctx.lineWidth = 2;
                ctx.beginPath();
                ctx.arc(node.x, node.y, 7, 0, Math.PI * 2);
                ctx.fill();
                ctx.stroke();

                // Node label
                ctx.fillStyle = '#94a3b8';
                ctx.font = '10px JetBrains Mono';
                ctx.fillText(node.name, node.x + 12, node.y + 4);
            }
        }

        // Main Animation Loop
        function simulationLoop() {
            const w = canvas.clientWidth;
            const h = canvas.clientHeight;

            if (canvas.width !== w * window.devicePixelRatio || canvas.height !== h * window.devicePixelRatio) {
                canvas.width = w * window.devicePixelRatio;
                canvas.height = h * window.devicePixelRatio;
                ctx.scale(window.devicePixelRatio, window.devicePixelRatio);
            }

            ctx.clearRect(0, 0, w, h);

            if (isRunning) {
                simulationTime += 1 * timeScale;
            }

            drawGalacticMap(w, h);

            requestAnimationFrame(simulationLoop);
        }

        window.onload = function() {
            addLog("Matriz SROS pronta. 15 nós estelares interconectados.");
            requestAnimationFrame(simulationLoop);
        };
    </script>
</body>
</html>
