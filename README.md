<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>METRIC ASSET GROUP | Premium Assets</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css" rel="stylesheet">
    <link rel="stylesheet" href="https://unpkg.com/aos@next/dist/aos.css" />
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Cinzel:wght@400;700;900&family=Inter:wght@300;400;600&display=swap');
        
        :root {
            --gold: #c5a059;
            --gold-bright: #e2c28a;
            --dark-bg: #0a0a0a;
            --panel-bg: rgba(12, 12, 12, 0.98);
            --error: #ff4d4d;
            --success: #4ade80;
        }

        body {
            font-family: 'Inter', sans-serif;
            background-color: var(--dark-bg);
            color: #d1d1d1;
            overflow-x: hidden;
            margin: 0;
        }

        .font-corp { font-family: 'Cinzel', serif; }

        .gold-text {
            background: linear-gradient(135deg, #c5a059 0%, #f1d5a2 50%, #8e6d31 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        /* Scrollbars */
        ::-webkit-scrollbar { width: 4px; }
        ::-webkit-scrollbar-track { background: #050505; }
        ::-webkit-scrollbar-thumb { background: var(--gold); border-radius: 10px; }

        #auth-screen, #payment-screen {
            background: radial-gradient(circle at center, #151515 0%, #050505 100%);
        }

        .input-premium {
            background: rgba(255,255,255,0.03);
            border: 1px solid rgba(197, 160, 89, 0.2);
            color: white;
            padding: 14px;
            width: 100%;
            transition: 0.3s;
            font-size: 11px;
            letter-spacing: 1px;
        }

        .input-premium:focus {
            border-color: var(--gold);
            outline: none;
            background: rgba(255,255,255,0.05);
        }

        .input-error {
            border-color: var(--error) !important;
            background: rgba(255, 77, 77, 0.05) !important;
        }

        /* Paneles Laterales */
        .side-panel {
            position: fixed;
            top: 0;
            height: 100vh;
            width: 280px;
            background: var(--panel-bg);
            border-right: 1px solid rgba(197, 160, 89, 0.2);
            z-index: 600;
            transition: transform 0.6s cubic-bezier(0.19, 1, 0.22, 1);
            display: flex;
            flex-direction: column;
            box-shadow: 20px 0 50px rgba(0,0,0,0.8);
        }

        .panel-header {
            padding: 30px 20px;
            border-bottom: 1px solid rgba(197, 160, 89, 0.1);
            display: flex;
            justify-content: space-between;
            align-items: center;
            background: rgba(0,0,0,0.2);
        }

        .panel-content {
            overflow-y: auto;
            flex: 1;
            padding: 10px 0;
        }

        #lang-panel { left: 0; transform: translateX(-100%); }
        #currency-panel { right: 0; transform: translateX(100%); border-right: none; border-left: 1px solid rgba(197, 160, 89, 0.2); }

        .panel-active#lang-panel, .panel-active#currency-panel { transform: translateX(0); }

        .panel-item {
            padding: 18px 25px;
            border-bottom: 1px solid rgba(255,255,255,0.03);
            cursor: pointer;
            transition: 0.3s;
            font-size: 0.7rem;
            text-transform: uppercase;
            letter-spacing: 1.5px;
            color: #777;
        }

        .panel-item:hover, .panel-item.active { 
            color: var(--gold); 
            background: rgba(197, 160, 89, 0.05); 
            border-left: 3px solid var(--gold);
        }

        .logo-hexagon {
            width: 45px;
            height: 50px;
            background: var(--gold);
            clip-path: polygon(50% 0%, 100% 25%, 100% 75%, 50% 100%, 0% 75%, 0% 25%);
            display: flex;
            align-items: center;
            justify-content: center;
            color: black;
            font-weight: 900;
        }

        .btn-premium {
            background: linear-gradient(90deg, #c5a059, #8e6d31);
            color: #000;
            font-weight: 700;
            text-transform: uppercase;
            letter-spacing: 1px;
            transition: 0.4s;
            cursor: pointer;
        }

        .btn-premium:disabled {
            opacity: 0.5;
            cursor: not-allowed;
        }

        .asset-card {
            background: #0f0f0f;
            border: 1px solid rgba(255,255,255,0.03);
            transition: 0.4s;
        }
        .asset-card:hover { transform: translateY(-5px); border-color: var(--gold); }

        #main-content { display: none; }
        .error-msg { color: var(--error); font-size: 9px; text-transform: uppercase; margin-top: 4px; display: none; }

        .dev-banner {
            background: rgba(197, 160, 89, 0.1);
            border-bottom: 1px solid var(--gold);
            padding: 8px;
            text-align: center;
            font-size: 9px;
            text-transform: uppercase;
            letter-spacing: 2px;
            color: var(--gold-bright);
            position: sticky;
            top: 0;
            z-index: 200;
        }

        /* Modal Animado */
        .modal-overlay {
            background: rgba(0,0,0,0.95);
            backdrop-filter: blur(10px);
        }
    </style>
</head>
<body>

    <!-- PANTALLA DE AUTENTICACIÓN -->
    <section id="auth-screen" class="fixed inset-0 z-[1000] flex items-center justify-center p-6">
        <div class="max-w-sm w-full text-center" data-aos="fade-up">
            <div class="logo-hexagon mx-auto mb-8 text-xl">M</div>
            <h1 class="font-corp gold-text text-2xl mb-2 tracking-[0.3em]" id="auth-title">METRIC LOGIN</h1>
            <p class="text-gray-500 text-[10px] uppercase tracking-[0.4em] mb-10" id="auth-subtitle">Acceso a Activos de Clase A</p>
            
            <div class="space-y-4 mb-8 text-left">
                <div>
                    <input type="text" id="login-user" placeholder="NOMBRE COMPLETO" class="input-premium tracking-widest uppercase">
                    <p id="err-user" class="error-msg">Este campo es obligatorio</p>
                </div>
                <div>
                    <input type="text" id="login-address" placeholder="DIRECCIÓN DE CUENTA / ENVÍO" class="input-premium tracking-widest uppercase">
                    <p id="err-address" class="error-msg">Se requiere dirección para envíos</p>
                </div>
                <div>
                    <input type="password" id="login-pass" placeholder="CLAVE DE ACCESO" class="input-premium tracking-widest uppercase">
                    <p id="err-pass" class="error-msg">Clave de seguridad requerida</p>
                </div>
            </div>
            
            <button onclick="handleLogin()" class="btn-premium w-full py-4 text-[10px] tracking-[0.2em]" id="btn-login">INICIAR SESIÓN</button>
            <p class="mt-6 text-[9px] text-gray-600 italic uppercase tracking-widest">Identidad protegida bajo protocolo THEMODS</p>
        </div>
    </section>

    <!-- PANTALLA DE PAGO (GOOGLE VERIFIED) -->
    <section id="payment-screen" class="fixed inset-0 z-[2000] hidden flex items-center justify-center p-6 modal-overlay">
        <div class="max-w-md w-full bg-neutral-950 border border-gold/30 p-8 shadow-2xl relative">
            <button onclick="closePayment()" class="absolute top-4 right-4 text-gray-500 hover:text-white"><i class="fa-solid fa-xmark"></i></button>
            
            <div class="text-center mb-8">
                <i class="fa-brands fa-google text-2xl mb-2 text-white"></i>
                <h2 class="font-corp gold-text text-xl tracking-widest">CHECKOUT SEGURO</h2>
                <p class="text-[8px] text-gray-500 uppercase tracking-widest">Verificado por Google Payments Security</p>
            </div>

            <div class="space-y-4">
                <div class="grid grid-cols-1 gap-4">
                    <input type="text" id="pay-card" placeholder="NÚMERO DE TARJETA (16 DÍGITOS)" class="input-premium tracking-[0.2em]" maxlength="16">
                    <input type="text" id="pay-name" placeholder="NOMBRE EN LA TARJETA" class="input-premium uppercase">
                </div>
                <div class="grid grid-cols-2 gap-4">
                    <input type="text" id="pay-expiry" placeholder="MM/YY" class="input-premium" maxlength="5">
                    <input type="password" id="pay-cvv" placeholder="CVV" class="input-premium" maxlength="3">
                </div>
            </div>

            <div class="mt-8 p-4 bg-white/5 border border-white/10">
                <div class="flex justify-between text-[10px] uppercase mb-2">
                    <span class="text-gray-400">Total a Autorizar:</span>
                    <span id="pay-total-display" class="text-gold font-bold">S/0.00</span>
                </div>
                <p class="text-[7px] text-gray-500 italic leading-relaxed">Al procesar, autoriza a METRIC ASSET GROUP a verificar la validez de los fondos. En caso de pago contra entrega, la tarjeta sirve como garantía de reserva.</p>
            </div>

            <button onclick="validateAndProcessPayment()" id="btn-confirm-pay" class="btn-premium w-full py-4 mt-6 text-[10px] tracking-widest">
                CONFIRMAR Y PAGAR
            </button>
            
            <div id="payment-loader" class="hidden mt-4 text-center">
                <div class="inline-block animate-spin rounded-full h-4 w-4 border-2 border-gold border-t-transparent"></div>
                <p class="text-[8px] text-gold mt-2 uppercase tracking-widest">Verificando con la entidad bancaria...</p>
            </div>
        </div>
    </section>

    <!-- MENSAJE DE ÉXITO -->
    <div id="success-modal" class="fixed inset-0 z-[3000] hidden flex items-center justify-center p-6 modal-overlay">
        <div class="max-w-sm w-full bg-neutral-950 border border-green-500/50 p-10 text-center shadow-2xl">
            <i class="fa-solid fa-circle-check text-5xl text-green-500 mb-6"></i>
            <h2 class="font-corp text-white text-2xl mb-4 tracking-widest">TRANSACCIÓN EXITOSA</h2>
            <p class="text-gray-400 text-xs leading-relaxed mb-8 uppercase tracking-tighter">
                Su pedido está en camino. <br> 
                <span class="text-white font-bold">Al llegar su pedido, por favor pague el monto total en efectivo o terminal.</span>
            </p>
            <button onclick="location.reload()" class="btn-premium px-8 py-3 text-[10px]">CERRAR TERMINAL</button>
        </div>
    </div>

    <!-- PANEL IDIOMAS -->
    <aside id="lang-panel" class="side-panel">
        <div class="panel-header">
            <h3 class="font-corp text-gold-bright text-xs tracking-widest uppercase">IDIOMA</h3>
            <button onclick="togglePanel('lang-panel')" class="text-gray-500 hover:text-white transition"><i class="fa-solid fa-xmark"></i></button>
        </div>
        <div class="panel-content">
            <div class="panel-item" onclick="setLang('es')">Español</div>
            <div class="panel-item" onclick="setLang('en')">English</div>
            <div class="panel-item" onclick="setLang('pt')">Português</div>
            <div class="panel-item" onclick="setLang('ru')">Русский</div>
            <div class="panel-item" onclick="setLang('fr')">Français</div>
            <div class="panel-item" onclick="setLang('de')">Deutsch</div>
            <div class="panel-item" onclick="setLang('it')">Italiano</div>
            <div class="panel-item" onclick="setLang('cn')">中文 (Chino)</div>
            <div class="panel-item" onclick="setLang('jp')">日本語 (Japonés)</div>
            <div class="panel-item" onclick="setLang('kr')">한국어 (Coreano)</div>
            <div class="panel-item" onclick="setLang('ar')">العربية (Árabe)</div>
        </div>
    </aside>

    <!-- PANEL DIVISAS -->
    <aside id="currency-panel" class="side-panel">
        <div class="panel-header">
            <button onclick="togglePanel('currency-panel')" class="text-gray-500 hover:text-white transition"><i class="fa-solid fa-xmark"></i></button>
            <h3 class="font-corp text-gold-bright text-xs tracking-widest uppercase">DIVISA</h3>
        </div>
        <div class="panel-content text-right">
            <div class="panel-item active" onclick="setCurrency('PEN', 1)">Sol Peruano (S/)</div>
            <div class="panel-item" onclick="setCurrency('USD', 0.27)">Dólar (USD)</div>
            <div class="panel-item" onclick="setCurrency('EUR', 0.25)">Euro (€)</div>
            <div class="panel-item" onclick="setCurrency('GBP', 0.21)">Libra (£)</div>
            <div class="panel-item" onclick="setCurrency('JPY', 40.5)">Yen (¥)</div>
            <div class="panel-item" onclick="setCurrency('BTC', 0.000003)">Bitcoin (₿)</div>
            <div class="panel-item" onclick="setCurrency('CHF', 0.24)">Franco Suizo (CHF)</div>
            <div class="panel-item" onclick="setCurrency('AUD', 0.42)">Dólar Aus (AUD)</div>
        </div>
    </aside>

    <!-- CONTENIDO PRINCIPAL -->
    <div id="main-content">
        <div class="dev-banner">
            <i class="fa-solid fa-triangle-exclamation mr-2"></i> 
            <span id="dev-text">Esta página está en desarrollo. Si encuentras un bug, no dudes en reportarlo.</span>
        </div>

        <nav class="sticky top-[31px] w-full z-[150] bg-black/95 border-b border-gold/20 py-5 px-8 flex justify-between items-center backdrop-blur-md">
            <div class="flex items-center gap-4">
                <div class="logo-hexagon">M</div>
                <div class="hidden md:flex flex-col">
                    <span class="text-lg font-corp gold-text tracking-widest">METRIC ASSET</span>
                    <span class="text-[7px] text-gray-500 tracking-[0.6em] uppercase">Global Enterprise</span>
                </div>
            </div>
            
            <div class="flex items-center space-x-8">
                <button onclick="togglePanel('lang-panel')" class="text-[10px] font-bold tracking-widest hover:text-gold transition uppercase" id="nav-lang">Idioma</button>
                <button onclick="togglePanel('currency-panel')" class="text-[10px] font-bold tracking-widest hover:text-gold transition uppercase" id="nav-curr">Divisa</button>
                <button onclick="toggleCart()" class="relative p-2 text-gold">
                    <i class="fa-solid fa-briefcase text-xl"></i>
                    <span id="cart-count" class="absolute -top-1 -right-1 bg-white text-black text-[9px] px-1.5 py-0.5 font-black">0</span>
                </button>
            </div>
        </nav>

        <header class="relative h-[60vh] flex items-center justify-center overflow-hidden">
            <img src="https://images.unsplash.com/photo-1486406146926-c627a92ad1ab?q=80&w=2000" class="absolute inset-0 w-full h-full object-cover opacity-20 grayscale">
            <div class="relative z-10 text-center px-4">
                <div class="inline-block border-y border-gold/40 py-2 mb-6" data-aos="zoom-in">
                    <p class="text-gold text-[8px] uppercase tracking-[1em]">Excellence In Every Asset</p>
                </div>
                <h1 class="text-5xl md:text-8xl font-corp gold-text mb-4 uppercase tracking-[0.2em]" id="hero-title">METRIC</h1>
                <p class="text-gray-500 text-[10px] uppercase font-bold tracking-[0.8em]" id="hero-subtitle">Assets & Entertainment Solutions</p>
            </div>
        </header>

        <main class="max-w-7xl mx-auto px-6 py-20">
            <section class="mb-24" id="section-games">
                <div class="flex flex-col md:flex-row justify-between items-end mb-12 border-l-4 border-gold pl-6">
                    <div>
                        <h2 class="font-corp text-3xl text-white uppercase tracking-widest" id="cat-exp-title">Catálogo de Experiencias</h2>
                        <p class="text-gold text-[10px] uppercase tracking-widest mt-2 font-bold" id="cat-exp-sub">Curaduría de Software</p>
                    </div>
                </div>
                <div id="games-grid" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8"></div>
            </section>

            <section class="mb-24" id="section-watches">
                <div class="flex flex-col md:flex-row justify-between items-end mb-12 border-l-4 border-gold pl-6">
                    <div>
                        <h2 class="font-corp text-3xl text-white uppercase tracking-widest" id="cat-wat-title">Relojería de Inversión</h2>
                        <p class="text-gold text-[10px] uppercase tracking-widest mt-2 font-bold" id="cat-wat-sub">Instrumentos de Precisión</p>
                    </div>
                </div>
                <div id="watches-grid" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6"></div>
            </section>

            <footer class="mt-32 pt-20 border-t border-white/5 text-center">
                <div class="logo-hexagon mx-auto mb-8 opacity-40">M</div>
                <p class="text-[9px] text-gray-600 uppercase tracking-[0.5em] mb-4">© 2026 Metric Asset Group - All Rights Reserved</p>
                <button onclick="reportBug()" class="text-gold text-[9px] uppercase tracking-widest hover:underline">
                    <i class="fa-solid fa-bug mr-2"></i> Reportar un error
                </button>
            </footer>
        </main>
    </div>

    <!-- Carrito -->
    <div id="cart-modal" class="fixed inset-0 z-[400] hidden">
        <div class="absolute inset-0 bg-black/95 backdrop-blur-lg" onclick="toggleCart()"></div>
        <div class="absolute right-0 top-0 h-full w-full max-w-md bg-neutral-950 p-10 border-l border-gold/30 flex flex-col shadow-2xl">
            <div class="flex justify-between items-center mb-10">
                <h2 class="font-corp text-2xl text-white uppercase tracking-tighter" id="cart-title">Portafolio</h2>
                <button onclick="toggleCart()" class="text-gray-500 hover:text-white transition"><i class="fa-solid fa-xmark text-xl"></i></button>
            </div>
            <div id="cart-items" class="space-y-6 overflow-y-auto flex-grow pr-4"></div>
            <div class="mt-10 pt-10 border-t border-white/10">
                <div class="flex justify-between mb-8">
                    <span class="text-xs uppercase text-gray-500 font-bold" id="total-val">Valuación</span>
                    <span id="cart-total" class="text-2xl font-corp gold-text">S/0.00</span>
                </div>
                <button onclick="openPayment()" class="btn-premium w-full py-5 text-xs tracking-widest" id="btn-final">FINALIZAR ADQUISICIÓN</button>
            </div>
        </div>
    </div>

    <script src="https://unpkg.com/aos@next/dist/aos.js"></script>
    <script>
        AOS.init({ duration: 800, once: true });
        let cart = [];
        let currentCurrency = 'PEN';
        let currentRate = 1;
        let currentLang = 'es';
        let currentUser = "";

        const i18n = {
            es: {
                dev: "Esta página está en desarrollo. Si encuentras un bug, no dudes en reportarlo.",
                lang: "Idioma", curr: "Divisa", hero: "METRIC", sub: "Assets & Entertainment Solutions",
                catExp: "Catálogo de Experiencias", catExpSub: "Curaduría de Software",
                catWat: "Relojería de Inversión", catWatSub: "Instrumentos de Precisión",
                soon: "Próximamente", cart: "Portafolio", total: "Valuación", final: "FINALIZAR ADQUISICIÓN",
                authTitle: "METRIC LOGIN", authSub: "Acceso a Activos de Clase A", btnLogin: "INICIAR SESIÓN",
                errUser: "Este campo es obligatorio", errAddr: "Se requiere dirección para envíos", errPass: "Clave de seguridad requerida",
                placeUser: "NOMBRE COMPLETO", placeAddr: "DIRECCIÓN DE CUENTA / ENVÍO", placePass: "CLAVE DE ACCESO"
            },
            en: {
                dev: "This page is in development. If you find a bug, don't hesitate to report it.",
                lang: "Language", curr: "Currency", hero: "METRIC", sub: "Assets & Entertainment Solutions",
                catExp: "Experience Catalog", catExpSub: "Software Curation",
                catWat: "Investment Watches", catWatSub: "Precision Instruments",
                soon: "Coming Soon", cart: "Portfolio", total: "Valuation", final: "FINALIZE ACQUISITION",
                authTitle: "METRIC LOGIN", authSub: "Class A Assets Access", btnLogin: "SIGN IN",
                errUser: "This field is mandatory", errAddr: "Shipping address required", errPass: "Security key required",
                placeUser: "FULL NAME", placeAddr: "ACCOUNT / SHIPPING ADDRESS", placePass: "ACCESS KEY"
            },
            // Otros idiomas cargados dinámicamente...
        };

        const assets = [
            { id: 1, type: 'game', tag: 'Militar', name: "Iron Resolve", price: 79, img: "https://images.unsplash.com/photo-1542751371-adc38448a05e" },
            { id: 2, type: 'game', tag: 'Historia', name: "The Last Dynasty", price: 55, img: "https://images.unsplash.com/photo-1552820728-8b83bb6b773f" },
            { id: 3, type: 'game', tag: 'Triste', name: "Echoes of Silence", price: 35, img: "https://images.unsplash.com/photo-1518709268805-4e9042af9f23" },
            { id: 4, type: 'game', tag: 'Acción', name: "Neon Vengeance", price: 65, img: "https://images.unsplash.com/photo-1550745165-9bc0b252726f" },
            { id: 101, type: 'watch', tag: 'Classic', name: "Metric Sovereign", price: 4500, img: "https://images.unsplash.com/photo-1524592094714-0f0654e20314" },
            { id: 102, type: 'watch', tag: 'Modern', name: "Onyx Horizon", price: 6200, img: "https://images.unsplash.com/photo-1522337360788-8b13dee7a37e" },
            { id: 103, type: 'watch', tag: 'Limited', name: "Aurum Spectre", price: 12500, img: "https://images.unsplash.com/photo-1539533018447-63fcce2678e3" }
        ];

        function handleLogin() {
            const user = document.getElementById('login-user');
            const addr = document.getElementById('login-address');
            const pass = document.getElementById('login-pass');
            let isValid = true;

            [user, addr, pass].forEach(el => el.classList.remove('input-error'));
            if(!user.value.trim()) { user.classList.add('input-error'); isValid = false; }
            if(!addr.value.trim()) { addr.classList.add('input-error'); isValid = false; }
            if(!pass.value.trim()) { pass.classList.add('input-error'); isValid = false; }

            if(isValid) {
                currentUser = user.value.trim();
                document.getElementById('auth-screen').style.opacity = '0';
                setTimeout(() => {
                    document.getElementById('auth-screen').style.display = 'none';
                    document.getElementById('main-content').style.display = 'block';
                    renderAssets();
                }, 500);
            }
        }

        // --- LÓGICA DE PAGO ---
        function openPayment() {
            if(cart.length === 0) return;
            const total = cart.reduce((acc, curr) => acc + curr.price, 0);
            document.getElementById('pay-total-display').innerText = formatPrice(total);
            document.getElementById('payment-screen').classList.remove('hidden');
            document.getElementById('pay-name').value = currentUser; // Autocompletar con nombre real
        }

        function closePayment() {
            document.getElementById('payment-screen').classList.add('hidden');
        }

        function validateAndProcessPayment() {
            const card = document.getElementById('pay-card').value;
            const name = document.getElementById('pay-name').value;
            const expiry = document.getElementById('pay-expiry').value;
            const cvv = document.getElementById('pay-cvv').value;
            const btn = document.getElementById('btn-confirm-pay');
            const loader = document.getElementById('payment-loader');

            // Reset errores
            document.querySelectorAll('#payment-screen .input-premium').forEach(i => i.classList.remove('input-error'));

            // Validaciones básicas de campos vacíos y longitud
            let valid = true;
            if(card.length < 16) { document.getElementById('pay-card').classList.add('input-error'); valid = false; }
            if(!name.trim()) { document.getElementById('pay-name').classList.add('input-error'); valid = false; }
            if(expiry.length < 5) { document.getElementById('pay-expiry').classList.add('input-error'); valid = false; }
            if(cvv.length < 3) { document.getElementById('pay-cvv').classList.add('input-error'); valid = false; }

            if(!valid) return;

            // Simulación de procesamiento
            btn.disabled = true;
            loader.classList.remove('hidden');

            setTimeout(() => {
                // Simulación de "Google Verification"
                loader.classList.add('hidden');
                document.getElementById('payment-screen').classList.add('hidden');
                document.getElementById('success-modal').classList.remove('hidden');
            }, 3000);
        }

        function setLang(code) {
            currentLang = code;
            const lang = i18n[code] || i18n.en;
            document.getElementById('dev-text').innerText = lang.dev;
            document.getElementById('nav-lang').innerText = lang.lang;
            document.getElementById('nav-curr').innerText = lang.curr;
            document.getElementById('hero-title').innerText = lang.hero;
            document.getElementById('cat-exp-title').innerText = lang.catExp;
            togglePanel('lang-panel');
        }

        function setCurrency(code, rate) {
            currentCurrency = code;
            currentRate = rate;
            renderAssets();
            updateCartUI();
            togglePanel('currency-panel');
        }

        function formatPrice(val) {
            const syms = { PEN: 'S/', USD: '$', EUR: '€', GBP: '£', JPY: '¥', BTC: '₿', CHF: 'CHF', AUD: 'A$' };
            const converted = val * currentRate;
            return `${syms[currentCurrency]}${converted.toLocaleString(undefined, { minimumFractionDigits: currentCurrency === 'BTC' ? 6 : 2 })}`;
        }

        function renderAssets() {
            const gamesGrid = document.getElementById('games-grid');
            const watchesGrid = document.getElementById('watches-grid');

            gamesGrid.innerHTML = assets.filter(a => a.type === 'game').map(g => `
                <div class="asset-card p-6 cursor-pointer group" onclick="addToCart(${g.id})">
                    <div class="h-64 overflow-hidden mb-6 bg-zinc-900 relative">
                        <img src="${g.img}" class="w-full h-full object-cover grayscale opacity-40 group-hover:opacity-100 group-hover:grayscale-0 group-hover:scale-110 transition duration-700">
                    </div>
                    <div class="flex justify-between items-center">
                        <h3 class="font-corp text-white text-md uppercase tracking-wider">${g.name}</h3>
                        <span class="text-xs font-bold text-white">${formatPrice(g.price)}</span>
                    </div>
                </div>
            `).join('');

            watchesGrid.innerHTML = assets.filter(a => a.type === 'watch').map(w => `
                <div class="asset-card p-4 cursor-pointer group" onclick="addToCart(${w.id})">
                    <div class="h-60 overflow-hidden mb-5 bg-zinc-900">
                        <img src="${w.img}" class="w-full h-full object-cover opacity-60 group-hover:opacity-100 transition duration-700">
                    </div>
                    <h3 class="font-corp text-white text-[11px] uppercase tracking-widest">${w.name}</h3>
                    <p class="text-gold text-sm font-black mt-3">${formatPrice(w.price)}</p>
                </div>
            `).join('');
        }

        function togglePanel(id) {
            const p = document.getElementById(id);
            p.classList.toggle('panel-active');
        }

        function toggleCart() {
            const m = document.getElementById('cart-modal');
            m.style.display = m.style.display === 'block' ? 'none' : 'block';
        }

        function addToCart(id) {
            const item = assets.find(a => a.id === id);
            cart.push(item);
            updateCartUI();
        }

        function removeFromCart(index) {
            cart.splice(index, 1);
            updateCartUI();
        }

        function updateCartUI() {
            document.getElementById('cart-count').innerText = cart.length;
            const container = document.getElementById('cart-items');
            const total = cart.reduce((acc, curr) => acc + curr.price, 0);
            container.innerHTML = cart.map((item, index) => `
                <div class="flex justify-between items-center border-b border-white/5 pb-5">
                    <div>
                        <p class="font-corp text-white text-[10px] uppercase">${item.name}</p>
                        <p class="text-[9px] text-gold mt-1">${formatPrice(item.price)}</p>
                    </div>
                    <button onclick="removeFromCart(${index})" class="text-gray-700 hover:text-red-500"><i class="fa-solid fa-trash-can"></i></button>
                </div>
            `).join('');
            document.getElementById('cart-total').innerText = formatPrice(total);
        }

        function reportBug() {
            alert("Terminal Metric: Reporte enviado a soporte central.");
        }
    </script>
</body>
</html>
