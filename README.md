<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>VisualDev Studio | AvaRute</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link
        href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700;800&family=Fira+Code:wght@400;500&display=swap"
        rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

    <style>
        :root {
            --neon-purple: #b53471;
            --neon-blue: #00f2fe;
            --dark-bg: #0a0a0f;
            --glass-bg: rgba(255, 255, 255, 0.03);
            --glass-border: rgba(255, 255, 255, 0.08);
        }

        body {
            background-color: var(--dark-bg);
            color: #e2e8f0;
            font-family: 'Poppins', sans-serif;
            overflow-x: hidden;
            cursor: none;
            /* Custom cursor */
        }

        .font-mono {
            font-family: 'Fira Code', monospace;
        }

        /* Glassmorphism Styles */
        .glass-panel {
            background: var(--glass-bg);
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
            border: 1px solid var(--glass-border);
            box-shadow: 0 8px 32px 0 rgba(0, 0, 0, 0.37);
        }

        /* Text Gradients */
        .text-gradient {
            background: linear-gradient(135deg, var(--neon-blue), #8a2be2, var(--neon-purple));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            background-size: 200% auto;
            animation: textShine 4s linear infinite;
        }

        @keyframes textShine {
            0% {
                background-position: 0% center;
            }

            100% {
                background-position: 200% center;
            }
        }

        /* Floating Animation */
        .float-anim {
            animation: float 6s ease-in-out infinite;
        }

        @keyframes float {
            0% {
                transform: translateY(0px);
            }

            50% {
                transform: translateY(-15px);
            }

            100% {
                transform: translateY(0px);
            }
        }

        /* Glow effects */
        .glow-hover {
            transition: all 0.3s ease;
        }

        .glow-hover:hover {
            box-shadow: 0 0 20px rgba(138, 43, 226, 0.5);
            border-color: rgba(138, 43, 226, 0.5);
        }

        /* Tech Stack 3D Container */
        .tilt-container {
            perspective: 1000px;
            transform-style: preserve-3d;
        }

        .tilt-card {
            transition: transform 0.1s ease, box-shadow 0.3s ease;
            transform-style: preserve-3d;
        }

        .tilt-card:hover {
            z-index: 10;
        }

        .tilt-content {
            transform: translateZ(30px);
            /* Pops the content out in 3D space */
        }

        /* Custom Scrollbar */
        ::-webkit-scrollbar {
            width: 8px;
        }

        ::-webkit-scrollbar-track {
            background: var(--dark-bg);
        }

        ::-webkit-scrollbar-thumb {
            background: linear-gradient(var(--neon-blue), var(--neon-purple));
            border-radius: 4px;
        }

        /* Custom Cursor */
        .custom-cursor {
            width: 20px;
            height: 20px;
            border: 2px solid var(--neon-blue);
            border-radius: 50%;
            position: fixed;
            pointer-events: none;
            z-index: 9999;
            transform: translate(-50%, -50%);
            transition: width 0.2s, height 0.2s, background-color 0.2s;
            box-shadow: 0 0 10px var(--neon-blue);
        }

        .custom-cursor.active {
            width: 40px;
            height: 40px;
            background-color: rgba(0, 242, 254, 0.2);
            border-color: var(--neon-purple);
            box-shadow: 0 0 15px var(--neon-purple);
        }

        .cursor-dot {
            width: 4px;
            height: 4px;
            background: var(--neon-purple);
            border-radius: 50%;
            position: fixed;
            pointer-events: none;
            z-index: 10000;
            transform: translate(-50%, -50%);
        }

        /* Anime Image container setup */
        .anime-container::before {
            content: '';
            position: absolute;
            inset: -2px;
            background: linear-gradient(45deg, var(--neon-blue), var(--neon-purple), var(--neon-blue));
            z-index: -1;
            border-radius: inherit;
            animation: gradientBorder 3s linear infinite;
        }

        @keyframes gradientBorder {
            0% {
                background-position: 0% 0%;
            }

            50% {
                background-position: 100% 100%;
            }

            100% {
                background-position: 0% 0%;
            }
        }
    </style>
</head>

<body class="antialiased selection:bg-purple-500 selection:text-white">

    <!-- Background Canvas -->
    <canvas id="particleCanvas" class="fixed top-0 left-0 w-full h-full -z-10 pointer-events-none opacity-60"></canvas>

    <!-- Custom Cursors -->
    <div id="cursor" class="custom-cursor hidden md:block"></div>
    <div id="cursor-dot" class="cursor-dot hidden md:block"></div>

    <div class="max-w-6xl mx-auto px-6 py-12 relative z-10">

        <!-- Hero Section -->
        <header class="flex flex-col lg:flex-row items-center justify-between gap-12 mb-20">
            <!-- Left Info -->
            <div class="flex-1 space-y-6">
                <div class="flex items-center gap-4 mb-2">
                    <div
                        class="w-20 h-20 md:w-24 md:h-24 rounded-full glass-panel flex items-center justify-center p-1 relative group cursor-hover">
                        <div
                            class="absolute inset-0 rounded-full border-2 border-transparent border-t-purple-500 animate-spin group-hover:border-t-blue-400">
                        </div>
                        <!-- Placeholder Avatar similar to the screenshot -->
                        <div
                            class="w-full h-full bg-[#a855f7] rounded-full flex flex-col items-center justify-center overflow-hidden">
                            <div class="w-3/4 h-1/2 bg-white rounded-t-xl mb-1"></div>
                            <div class="flex gap-2 w-3/4 h-1/4">
                                <div class="w-1/2 h-full bg-white rounded-md"></div>
                                <div class="w-1/2 h-full bg-white rounded-md"></div>
                            </div>
                        </div>
                    </div>
                    <div>
                        <h2 class="text-xl text-gray-400 font-mono">@visualdev-studio</h2>
                        <span
                            class="inline-flex items-center gap-2 px-3 py-1 mt-1 rounded-full text-xs font-semibold bg-green-500/10 text-green-400 border border-green-500/20">
                            <i class="fas fa-circle text-[8px] animate-pulse"></i> Just Wanted
                        </span>
                    </div>
                </div>

                <h1 class="text-5xl md:text-6xl font-bold tracking-tight">
                    Hi there, I'm <br />
                    <span class="text-gradient">VisualDev Studio</span> <span
                        class="animate-[wave_2s_ease-in-out_infinite] inline-block origin-bottom-right">👋</span>
                </h1>

                <h3 class="text-xl md:text-2xl font-medium text-gray-300">
                    <span class="text-blue-400 font-mono">&lt;</span>
                    Creative Front-End Developer & UI/UX Enthusiast
                    <span class="text-blue-400 font-mono">/&gt;</span> 🎨 💻
                </h3>

                <div class="flex gap-4 pt-4">
                    <button
                        class="cursor-hover glass-panel px-6 py-3 rounded-lg font-semibold flex items-center gap-2 hover:bg-white/10 transition-colors border border-purple-500/30 hover:border-purple-500 text-white group">
                        <i class="fas fa-user-edit group-hover:text-purple-400 transition-colors"></i> Edit Profile Mock
                    </button>
                    <button
                        class="cursor-hover glass-panel px-6 py-3 rounded-lg font-semibold flex items-center gap-2 hover:bg-white/10 transition-colors border border-blue-500/30 hover:border-blue-500 text-white group">
                        <i class="fas fa-paper-plane group-hover:text-blue-400 transition-colors"></i> Mari Terhubung
                    </button>
                </div>
            </div>

            <!-- Right Anime Lofi Animation -->
            <div class="flex-1 flex justify-center w-full max-w-md lg:max-w-none relative">
                <!-- Floating decorative elements -->
                <div class="absolute -top-10 -left-10 w-24 h-24 bg-blue-500/20 rounded-full blur-2xl animate-pulse">
                </div>
                <div class="absolute -bottom-10 -right-10 w-32 h-32 bg-purple-500/20 rounded-full blur-2xl animate-pulse"
                    style="animation-delay: 1s;"></div>

                <div
                    class="relative anime-container rounded-2xl float-anim w-full aspect-video shadow-[0_0_40px_rgba(138,43,226,0.3)] p-1 z-10 cursor-hover">
                    <div class="w-full h-full rounded-2xl overflow-hidden relative glass-panel">
                        <!-- High quality aesthetic lofi studying GIF placeholder -->
                        <img src="https://media.tenor.com/Fw8_c1bM7b0AAAAC/lofi-girl.gif" alt="Anime Studying"
                            class="w-full h-full object-cover opacity-80 mix-blend-screen" />

                        <!-- Overlay gradient to blend it into the dark theme -->
                        <div class="absolute inset-0 bg-gradient-to-t from-[#0a0a0f] via-transparent to-transparent">
                        </div>

                        <!-- Floating interactive code snippets -->
                        <div class="absolute bottom-4 left-4 glass-panel px-3 py-2 rounded-md text-xs font-mono text-purple-300 border-l-4 border-purple-500 float-anim"
                            style="animation-duration: 4s;">
                            const state = 'learning';
                        </div>
                        <div class="absolute top-4 right-4 glass-panel px-3 py-2 rounded-md text-xs font-mono text-blue-300 border-l-4 border-blue-500 float-anim"
                            style="animation-duration: 5s; animation-delay: 1s;">
                            <i class="fas fa-code"></i> compile_success
                        </div>
                    </div>
                </div>
            </div>
        </header>

        <!-- Main Grid Layout -->
        <div class="grid grid-cols-1 lg:grid-cols-12 gap-8">

            <!-- Left Column (About & Connections) -->
            <div class="lg:col-span-5 space-y-8">

                <!-- About Section -->
                <section class="glass-panel rounded-2xl p-6 glow-hover group">
                    <h3 class="text-xl font-bold mb-4 flex items-center gap-3">
                        <i class="fas fa-user-astronaut text-purple-400 group-hover:animate-bounce"></i>
                        Tentang Saya
                    </h3>
                    <p class="text-gray-300 leading-relaxed text-sm md:text-base">
                        Saya berfokus pada menjembatani kesenjangan antara desain antarmuka yang indah (Figma) dan kode
                        yang bersih serta interaktif. Saya senang mengubah ide dan wireframe menjadi pengalaman digital
                        yang nyata.
                    </p>
                    <div class="mt-6 space-y-2 text-sm text-gray-400">
                        <div class="flex items-center gap-2 hover:text-white transition-colors cursor-hover">
                            <i class="fas fa-map-marker-alt w-5 text-center text-blue-400"></i> Anywhere (Remote)
                        </div>
                    </div>
                </section>

                <!-- Connection / Links Section -->
                <section class="glass-panel rounded-2xl p-6 glow-hover">
                    <h3 class="text-xl font-bold mb-5 flex items-center gap-3">
                        <i class="fas fa-link text-blue-400"></i> Mari Terhubung
                    </h3>
                    <ul class="space-y-4">
                        <li>
                            <a href="#"
                                class="cursor-hover flex items-center gap-4 p-3 rounded-xl hover:bg-white/5 transition-all border border-transparent hover:border-white/10 group">
                                <div
                                    class="w-10 h-10 rounded-lg bg-[#0e76a8]/20 flex items-center justify-center text-[#0e76a8] group-hover:bg-[#0e76a8] group-hover:text-white transition-all">
                                    <i class="fab fa-linkedin-in text-lg"></i>
                                </div>
                                <div>
                                    <h4 class="font-semibold text-white group-hover:text-[#0e76a8] transition-colors">
                                        LinkedIn</h4>
                                    <p class="text-xs text-gray-400">in/mochalfianabadirochim</p>
                                </div>
                            </a>
                        </li>
                        <li>
                            <a href="#"
                                class="cursor-hover flex items-center gap-4 p-3 rounded-xl hover:bg-white/5 transition-all border border-transparent hover:border-white/10 group">
                                <div
                                    class="w-10 h-10 rounded-lg bg-gradient-to-tr from-[#f09433] via-[#dc2743] to-[#bc1888] opacity-80 flex items-center justify-center text-white group-hover:opacity-100 transition-all">
                                    <i class="fab fa-instagram text-lg"></i>
                                </div>
                                <div>
                                    <h4 class="font-semibold text-white group-hover:text-[#dc2743] transition-colors">
                                        Instagram</h4>
                                    <p class="text-xs text-gray-400">@alfian_ab76</p>
                                </div>
                            </a>
                        </li>
                        <li>
                            <a href="#"
                                class="cursor-hover flex items-center gap-4 p-3 rounded-xl hover:bg-white/5 transition-all border border-transparent hover:border-white/10 group">
                                <div
                                    class="w-10 h-10 rounded-lg bg-[#ea4c89]/20 flex items-center justify-center text-[#ea4c89] group-hover:bg-[#ea4c89] group-hover:text-white transition-all">
                                    <i class="fab fa-dribbble text-lg"></i>
                                </div>
                                <div>
                                    <h4 class="font-semibold text-white group-hover:text-[#ea4c89] transition-colors">
                                        Dribbble</h4>
                                    <p class="text-xs text-gray-400">UI/UX Portfolio</p>
                                </div>
                            </a>
                        </li>
                    </ul>
                </section>
            </div>

            <!-- Right Column (Tech Stack & Stats) -->
            <div class="lg:col-span-7 space-y-8">

                <!-- Tech Stack Section -->
                <section class="glass-panel rounded-2xl p-6 glow-hover">
                    <h3 class="text-xl font-bold mb-6 flex items-center gap-3">
                        <i class="fas fa-layer-group text-purple-400"></i> Tech Stack & Tools
                    </h3>

                    <div class="grid grid-cols-2 sm:grid-cols-3 gap-4 tilt-container" id="tech-stack-container">
                        <!-- Figma -->
                        <div
                            class="tilt-card glass-panel rounded-xl p-4 flex flex-col items-center justify-center gap-3 cursor-hover border border-white/5 hover:border-[#F24E1E]/50 group h-32 relative overflow-hidden">
                            <div
                                class="absolute inset-0 bg-gradient-to-br from-[#F24E1E]/20 to-transparent opacity-0 group-hover:opacity-100 transition-opacity">
                            </div>
                            <div class="tilt-content flex flex-col items-center">
                                <i
                                    class="fab fa-figma text-4xl text-[#F24E1E] group-hover:scale-110 transition-transform shadow-glow"></i>
                                <span class="mt-2 font-mono text-sm font-semibold tracking-wide">FIGMA</span>
                            </div>
                        </div>

                        <!-- HTML5 -->
                        <div
                            class="tilt-card glass-panel rounded-xl p-4 flex flex-col items-center justify-center gap-3 cursor-hover border border-white/5 hover:border-[#E34F26]/50 group h-32 relative overflow-hidden">
                            <div
                                class="absolute inset-0 bg-gradient-to-br from-[#E34F26]/20 to-transparent opacity-0 group-hover:opacity-100 transition-opacity">
                            </div>
                            <div class="tilt-content flex flex-col items-center">
                                <i
                                    class="fab fa-html5 text-4xl text-[#E34F26] group-hover:scale-110 transition-transform shadow-glow"></i>
                                <span class="mt-2 font-mono text-sm font-semibold tracking-wide">HTML5</span>
                            </div>
                        </div>

                        <!-- CSS3 -->
                        <div
                            class="tilt-card glass-panel rounded-xl p-4 flex flex-col items-center justify-center gap-3 cursor-hover border border-white/5 hover:border-[#1572B6]/50 group h-32 relative overflow-hidden">
                            <div
                                class="absolute inset-0 bg-gradient-to-br from-[#1572B6]/20 to-transparent opacity-0 group-hover:opacity-100 transition-opacity">
                            </div>
                            <div class="tilt-content flex flex-col items-center">
                                <i
                                    class="fab fa-css3-alt text-4xl text-[#1572B6] group-hover:scale-110 transition-transform shadow-glow"></i>
                                <span class="mt-2 font-mono text-sm font-semibold tracking-wide">CSS3</span>
                            </div>
                        </div>

                        <!-- Tailwind CSS -->
                        <div
                            class="tilt-card glass-panel rounded-xl p-4 flex flex-col items-center justify-center gap-3 cursor-hover border border-white/5 hover:border-[#38B2AC]/50 group h-32 relative overflow-hidden">
                            <div
                                class="absolute inset-0 bg-gradient-to-br from-[#38B2AC]/20 to-transparent opacity-0 group-hover:opacity-100 transition-opacity">
                            </div>
                            <div class="tilt-content flex flex-col items-center">
                                <svg class="w-10 h-10 text-[#38B2AC] group-hover:scale-110 transition-transform"
                                    fill="currentColor" viewBox="0 0 24 24">
                                    <path
                                        d="M12.001 4.8c-3.2 0-5.2 1.6-6 4.8 1.2-1.6 2.6-2.2 4.2-1.8.913.228 1.565.89 2.288 1.624C13.666 10.618 15.027 12 18.001 12c3.2 0 5.2-1.6 6-4.8-1.2 1.6-2.6 2.2-4.2 1.8-.913-.228-1.565-.89-2.288-1.624C16.337 6.182 14.976 4.8 12.001 4.8zm-6 7.2c-3.2 0-5.2 1.6-6 4.8 1.2-1.6 2.6-2.2 4.2-1.8.913.228 1.565.89 2.288 1.624 1.177 1.194 2.538 2.576 5.512 2.576 3.2 0 5.2-1.6 6-4.8-1.2 1.6-2.6 2.2-4.2 1.8-.913-.228-1.565-.89-2.288-1.624C10.337 13.382 8.976 12 6.001 12z" />
                                </svg>
                                <span class="mt-2 font-mono text-sm font-semibold tracking-wide">TAILWIND</span>
                            </div>
                        </div>

                        <!-- JavaScript -->
                        <div
                            class="tilt-card glass-panel rounded-xl p-4 flex flex-col items-center justify-center gap-3 cursor-hover border border-white/5 hover:border-[#F7DF1E]/50 group h-32 relative overflow-hidden">
                            <div
                                class="absolute inset-0 bg-gradient-to-br from-[#F7DF1E]/20 to-transparent opacity-0 group-hover:opacity-100 transition-opacity">
                            </div>
                            <div class="tilt-content flex flex-col items-center">
                                <i
                                    class="fab fa-js text-4xl text-[#F7DF1E] group-hover:scale-110 transition-transform shadow-glow"></i>
                                <span class="mt-2 font-mono text-sm font-semibold tracking-wide">JAVASCRIPT</span>
                            </div>
                        </div>

                        <!-- React -->
                        <div
                            class="tilt-card glass-panel rounded-xl p-4 flex flex-col items-center justify-center gap-3 cursor-hover border border-white/5 hover:border-[#61DAFB]/50 group h-32 relative overflow-hidden">
                            <div
                                class="absolute inset-0 bg-gradient-to-br from-[#61DAFB]/20 to-transparent opacity-0 group-hover:opacity-100 transition-opacity">
                            </div>
                            <div class="tilt-content flex flex-col items-center">
                                <i
                                    class="fab fa-react text-4xl text-[#61DAFB] group-hover:scale-110 transition-transform animate-[spin_10s_linear_infinite] group-hover:animate-[spin_3s_linear_infinite]"></i>
                                <span class="mt-2 font-mono text-sm font-semibold tracking-wide">REACT</span>
                            </div>
                        </div>
                    </div>
                </section>

                <!-- GitHub Stats Section -->
                <section class="glass-panel rounded-2xl p-6 glow-hover">
                    <h3 class="text-xl font-bold mb-6 flex items-center gap-3">
                        <i class="fab fa-github text-white"></i> GitHub Stats
                    </h3>

                    <div class="grid grid-cols-1 sm:grid-cols-3 gap-4">
                        <!-- Stat Box 1 -->
                        <div
                            class="glass-panel rounded-xl p-5 border-t-2 border-t-purple-500 relative overflow-hidden group cursor-hover">
                            <div
                                class="absolute -right-4 -top-4 w-16 h-16 bg-purple-500/10 rounded-full blur-xl group-hover:bg-purple-500/30 transition-all">
                            </div>
                            <div class="flex flex-col">
                                <span class="text-gray-400 text-sm font-medium mb-1">Total Repositories</span>
                                <span class="text-4xl font-bold text-white tracking-tight stat-counter"
                                    data-target="42">0</span>
                            </div>
                        </div>

                        <!-- Stat Box 2 -->
                        <div
                            class="glass-panel rounded-xl p-5 border-t-2 border-t-blue-500 relative overflow-hidden group cursor-hover">
                            <div
                                class="absolute -right-4 -top-4 w-16 h-16 bg-blue-500/10 rounded-full blur-xl group-hover:bg-blue-500/30 transition-all">
                            </div>
                            <div class="flex flex-col">
                                <span class="text-gray-400 text-sm font-medium mb-1">Total Stars</span>
                                <span class="text-4xl font-bold text-white tracking-tight stat-counter"
                                    data-target="128">0</span>
                            </div>
                        </div>

                        <!-- Stat Box 3 -->
                        <div
                            class="glass-panel rounded-xl p-5 border-t-2 border-t-green-500 relative overflow-hidden group cursor-hover">
                            <div
                                class="absolute -right-4 -top-4 w-16 h-16 bg-green-500/10 rounded-full blur-xl group-hover:bg-green-500/30 transition-all">
                            </div>
                            <div class="flex flex-col">
                                <span class="text-gray-400 text-sm font-medium mb-1">Total Commits</span>
                                <span class="text-4xl font-bold text-white tracking-tight stat-counter"
                                    data-target="1043">0</span>
                            </div>
                        </div>
                    </div>

                    <!-- Decorative mock contribution graph -->
                    <div class="mt-6 p-4 bg-black/40 rounded-xl border border-white/5 hidden md:block">
                        <div class="text-xs text-gray-500 mb-2">Contribution Graph (Mock)</div>
                        <div class="flex gap-1 flex-wrap" id="contrib-graph">
                            <!-- JS will populate tiny squares here -->
                        </div>
                    </div>
                </section>
            </div>
        </div>

        <footer class="mt-20 text-center text-sm text-gray-500 pb-8">
            <p>Designed with <i class="fas fa-heart text-purple-500 animate-pulse"></i> by VisualDev Studio &copy; <span
                    id="year"></span></p>
        </footer>
    </div>

    <script>
        // Update year
        document.getElementById('year').textContent = new Date().getFullYear();

        // Custom Cursor Logic
        const cursor = document.getElementById('cursor');
        const cursorDot = document.getElementById('cursor-dot');
        const hoverElements = document.querySelectorAll('.cursor-hover, button, a');

        // Only run on desktop devices to prevent mobile touch issues
        if (window.matchMedia("(pointer: fine)").matches) {
            window.addEventListener('mousemove', (e) => {
                const posX = e.clientX;
                const posY = e.clientY;

                // Use requestAnimationFrame for smoother movement
                requestAnimationFrame(() => {
                    cursor.style.left = `${posX}px`;
                    cursor.style.top = `${posY}px`;

                    cursorDot.style.left = `${posX}px`;
                    cursorDot.style.top = `${posY}px`;
                });
            });

            hoverElements.forEach(el => {
                el.addEventListener('mouseenter', () => {
                    cursor.classList.add('active');
                });
                el.addEventListener('mouseleave', () => {
                    cursor.classList.remove('active');
                });
            });
        }

        // 3D Tilt Effect for Tech Stack Cards
        const tiltCards = document.querySelectorAll('.tilt-card');

        tiltCards.forEach(card => {
            card.addEventListener('mousemove', (e) => {
                const rect = card.getBoundingClientRect();
                const x = e.clientX - rect.left; // x position within the element.
                const y = e.clientY - rect.top;  // y position within the element.

                const centerX = rect.width / 2;
                const centerY = rect.height / 2;

                const rotateX = ((y - centerY) / centerY) * -15; // Max rotation 15deg
                const rotateY = ((x - centerX) / centerX) * 15;

                card.style.transform = `perspective(1000px) rotateX(${rotateX}deg) rotateY(${rotateY}deg)`;
            });

            card.addEventListener('mouseleave', () => {
                card.style.transform = `perspective(1000px) rotateX(0) rotateY(0)`;
            });
        });

        // Animated Statistics Counter
        const counters = document.querySelectorAll('.stat-counter');
        const speed = 200; // Lower is faster

        const animateCounters = () => {
            counters.forEach(counter => {
                const updateCount = () => {
                    const target = +counter.getAttribute('data-target');
                    const count = +counter.innerText;
                    const inc = target / speed;

                    if (count < target) {
                        counter.innerText = Math.ceil(count + inc);
                        setTimeout(updateCount, 15);
                    } else {
                        counter.innerText = target;
                    }
                };
                updateCount();
            });
        };

        // Simple Intersection Observer to start counter when visible
        const observer = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    animateCounters();
                    observer.unobserve(entry.target);
                }
            });
        }, { threshold: 0.5 });

        counters.forEach(counter => observer.observe(counter));

        // Generate Mock Contribution Graph
        const graphContainer = document.getElementById('contrib-graph');
        if (graphContainer) {
            const colors = ['bg-gray-800', 'bg-purple-900/40', 'bg-purple-700/60', 'bg-purple-500', 'bg-blue-400'];
            for (let i = 0; i < 156; i++) {
                const box = document.createElement('div');
                box.className = `w-3 h-3 rounded-sm ${colors[Math.floor(Math.random() * colors.length)]} hover:scale-150 hover:z-10 transition-transform cursor-pointer`;
                graphContainer.appendChild(box);
            }
        }

        // Interactive Canvas Particle Background Network
        const canvas = document.getElementById('particleCanvas');
        const ctx = canvas.getContext('2d');
        let particlesArray;

        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;

        let mouse = {
            x: null,
            y: null,
            radius: (canvas.height / 8) * (canvas.width / 8)
        }

        window.addEventListener('mousemove', function (event) {
            mouse.x = event.x;
            mouse.y = event.y;
        });

        window.addEventListener('mouseout', function () {
            mouse.x = null;
            mouse.y = null;
        });

        class Particle {
            constructor(x, y, directionX, directionY, size, color) {
                this.x = x;
                this.y = y;
                this.directionX = directionX;
                this.directionY = directionY;
                this.size = size;
                this.color = color;
            }

            draw() {
                ctx.beginPath();
                ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2, false);
                ctx.fillStyle = this.color;
                ctx.fill();
            }

            update() {
                if (this.x > canvas.width || this.x < 0) this.directionX = -this.directionX;
                if (this.y > canvas.height || this.y < 0) this.directionY = -this.directionY;

                // Check collision detection - mouse position / particle position
                let dx = mouse.x - this.x;
                let dy = mouse.y - this.y;
                let distance = Math.sqrt(dx * dx + dy * dy);

                if (distance < mouse.radius + this.size) {
                    if (mouse.x < this.x && this.x < canvas.width - this.size * 10) {
                        this.x += 3;
                    }
                    if (mouse.x > this.x && this.x > this.size * 10) {
                        this.x -= 3;
                    }
                    if (mouse.y < this.y && this.y < canvas.height - this.size * 10) {
                        this.y += 3;
                    }
                    if (mouse.y > this.y && this.y > this.size * 10) {
                        this.y -= 3;
                    }
                }

                this.x += this.directionX;
                this.y += this.directionY;
                this.draw();
            }
        }

        function init() {
            particlesArray = [];
            let numberOfParticles = (canvas.height * canvas.width) / 12000;
            // Limit max particles to maintain performance
            if (numberOfParticles > 100) numberOfParticles = 100;

            for (let i = 0; i < numberOfParticles; i++) {
                let size = (Math.random() * 2) + 1;
                let x = (Math.random() * ((innerWidth - size * 2) - (size * 2)) + size * 2);
                let y = (Math.random() * ((innerHeight - size * 2) - (size * 2)) + size * 2);
                let directionX = (Math.random() * 2) - 1;
                let directionY = (Math.random() * 2) - 1;
                // Mix of neon purple and blue colors for particles
                let color = Math.random() > 0.5 ? '#b53471' : '#00f2fe';

                particlesArray.push(new Particle(x, y, directionX, directionY, size, color));
            }
        }

        function connect() {
            let opacityValue = 1;
            for (let a = 0; a < particlesArray.length; a++) {
                for (let b = a; b < particlesArray.length; b++) {
                    let distance = ((particlesArray[a].x - particlesArray[b].x) * (particlesArray[a].x - particlesArray[b].x))
                        + ((particlesArray[a].y - particlesArray[b].y) * (particlesArray[a].y - particlesArray[b].y));

                    if (distance < (canvas.width / 7) * (canvas.height / 7)) {
                        opacityValue = 1 - (distance / 15000);
                        ctx.strokeStyle = `rgba(138, 43, 226, ${opacityValue * 0.2})`;
                        ctx.lineWidth = 1;
                        ctx.beginPath();
                        ctx.moveTo(particlesArray[a].x, particlesArray[a].y);
                        ctx.lineTo(particlesArray[b].x, particlesArray[b].y);
                        ctx.stroke();
                    }
                }
            }
        }

        function animate() {
            requestAnimationFrame(animate);
            ctx.clearRect(0, 0, innerWidth, innerHeight);
            for (let i = 0; i < particlesArray.length; i++) {
                particlesArray[i].update();
            }
            connect();
        }

        // Handle resize
        window.addEventListener('resize', function () {
            canvas.width = innerWidth;
            canvas.height = innerHeight;
            mouse.radius = ((canvas.height / 8) * (canvas.width / 8));
            init();
        });

        init();
        animate();
    </script>
</body>

</html>
