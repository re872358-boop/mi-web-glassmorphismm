# mi-web-glassmorphismm
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
    <title>LOBA Enterprise | Neural System</title>
    <script src="https://unpkg.com/@tailwindcss/browser@4"></script>
    <link rel="stylesheet" href="styles/style.css">
</head>
<body class="bg-[#020617] text-slate-300 antialiased overflow-x-hidden">

    <header class="fixed top-0 w-full z-50 glass-premium px-6 py-4 flex justify-between items-center border-b border-white/5">
        <div class="text-[10px] font-black tracking-[0.2em] text-white">
            NICOLÁS <span class="text-blue-500 italic">♊ LOBA v2.5</span>
        </div>
        <div class="h-2 w-2 rounded-full bg-emerald-500 animate-pulse shadow-[0_0_8px_#10b981]"></div>
    </header>

    <main class="pt-[60px]">
        <section class="relative h-[35vh] w-full overflow-hidden bg-slate-900">
            <img src="https://images.unsplash.com/photo-1518770660439-4636190af475?auto=format&fit=crop&q=80&w=1000" 
                 class="w-full h-full object-cover opacity-60" alt="Core Network">
            <div class="absolute inset-0 bg-gradient-to-t from-[#020617] via-transparent to-black/40"></div>
            <div class="absolute bottom-6 left-6">
                <h1 class="text-3xl font-black text-white italic tracking-tighter leading-none">
                    SISTEMA <br> <span class="text-blue-500">AUTÓNOMO</span>
                </h1>
            </div>
        </section>

        <section class="px-4 py-8 space-y-6">
            <h2 class="text-blue-500 font-mono text-[9px] tracking-[0.5em] uppercase text-center mb-4">Portfolio de Soluciones</h2>
            
            <div class="glass-premium p-5 rounded-3xl border-l-4 border-l-blue-500">
                <h4 class="text-white font-black italic text-sm mb-1">GAMING ENGINE v1.0</h4>
                <p class="text-[11px] text-slate-400 leading-relaxed">Software de entretenimiento de alta performance para entornos móviles.</p>
            </div>

            <div class="glass-premium p-5 rounded-3xl border-l-4 border-l-emerald-500">
                <h4 class="text-white font-black italic text-sm mb-1">GESTIÓN PRO</h4>
                <p class="text-[11px] text-slate-400 leading-relaxed">Sistemas de administración financiera y control de activos en tiempo real.</p>
            </div>
        </section>

        <section class="px-4 mb-8">
            <div class="glass-premium rounded-[2rem] overflow-hidden border border-blue-500/20">
                <div class="bg-blue-500/10 px-6 py-3 border-b border-white/5 flex items-center gap-3">
                    <div class="h-1.5 w-1.5 bg-blue-500 rounded-full animate-pulse"></div>
                    <span class="text-[8px] font-mono text-blue-400 tracking-widest uppercase">Loba_Neural_Agent_v2.5</span>
                </div>
                
                <div id="chat-window" class="h-40 overflow-y-auto p-5 space-y-3 text-[10px] font-mono leading-relaxed">
                    <div class="text-blue-300">
                        <span class="text-blue-500">>></span> Bienvenido al Búnker. Iniciando protocolo de asesoría estratégica... ¿En qué área necesitas potenciar tu estructura?
                    </div>
                </div>

                <div class="p-4 bg-black/40 border-t border-white/5 flex gap-2">
                    <input type="text" id="chat-input" placeholder="Consultar sobre Juegos o Gestión..." 
                           class="flex-1 bg-transparent border-none text-[11px] text-white focus:outline-none">
                    <button id="send-chat" class="text-blue-500 font-bold text-[10px] uppercase">Enviar</button>
                </div>
            </div>
        </section>

        <section class="px-4 pb-12">
            <div class="glass-premium p-6 rounded-[2.5rem]">
                <h3 class="text-white font-bold text-center mb-6 tracking-widest text-[9px] uppercase">Confirmar Adquisición</h3>
                <form id="order-form" class="space-y-4">
                    <input type="text" placeholder="Tu Nombre" class="w-full input-glass text-xs">
                    <select id="product-select" class="w-full input-glass text-xs bg-slate-900">
                        <option value="" disabled selected>Elegir producto...</option>
                        <option value="juegos">Gaming Engine v1.0</option>
                        <option value="gestion">Sistema Gestión Pro</option>
                    </select>
                    <button type="button" class="w-full btn-primary text-[10px] py-4">SOLICITAR AUDITORÍA</button>
                </form>
            </div>
        </section>
    </main>

    <script src="script.js/javscrip.js"></script>
</body>
</html>

const chatInput = document.getElementById('chat-input');
const chatWindow = document.getElementById('chat-window');
const sendBtn = document.getElementById('send-chat');

const iaResponses = {
    "juegos": "Nuestros Gaming Engines están optimizados para Android con C++ y baja latencia. El precio es bajo presupuesto y la demora es de 15 días. ¿Te interesa una auditoría?",
    "gestion": "El Sistema de Gestión Pro maneja intereses, cobros y stock en tiempo real. Se instala en 7 días y es 100% privado (IndexedDB).",
    "hola": "Saludos, Arquitecto. Soy el Agente Neural de Nicolás. ¿Buscas asesoramiento en Juegos, Gestión o Seguridad?"
};

function addMessage(text, isUser = false) {
    const msg = document.createElement('div');
    msg.innerHTML = `<span class="${isUser ? 'text-emerald-400' : 'text-blue-500'}">${isUser ? '> User:' : '>> IA:'}</span> ${text}`;
    chatWindow.appendChild(msg);
    chatWindow.scrollTop = chatWindow.scrollHeight;
}

sendBtn.onclick = () => {
    const prompt = chatInput.value.toLowerCase();
    if (!prompt) return;

    addMessage(chatInput.value, true);
    chatInput.value = '';

    setTimeout(() => {
        let response = "Análisis completado. No detecto ese módulo en el inventario actual. ¿Podrías ser más específico sobre Juegos o Gestión?";
        
        if (prompt.includes("juego")) response = iaResponses.juegos;
        else if (prompt.includes("gestion") || prompt.includes("prestamo")) response = iaResponses.gestion;
        else if (prompt.includes("hola")) response = iaResponses.hola;

        addMessage(response);
    }, 800);
};


/* LOBA ENTERPRISE - CORE STYLES v2.5
   Optimized for Xiaomi Redmi Note 13 (23100RN82L)
*/

:root {
    --bg-main: #020617;
    --enterprise: #3b82f6; /* Azul moderno */
    --loba-pink: #f43f5e;   /* Rosa/Rojo para alertas */
    --glass: rgba(15, 23, 42, 0.65);
    --glass-border: rgba(255, 255, 255, 0.08);
}

/* Reseteo Senior */
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    -webkit-tap-highlight-color: transparent;
}

body {
    background-color: var(--bg-main);
    font-family: 'Inter', -apple-system, sans-serif;
    color: #cbd5e1;
    line-height: 1.5;
    overflow-x: hidden;
}

/* Efecto Glassmorphism Premium */
.glass-premium {
    background: var(--glass);
    backdrop-filter: blur(16px) saturate(180%);
    -webkit-backdrop-filter: blur(16px) saturate(180%);
    border: 1px solid var(--glass-border);
    box-shadow: 0 8px 32px 0 rgba(0, 0, 0, 0.37);
}

/* Animaciones para 120Hz */
@keyframes fadeIn {
    from { opacity: 0; transform: translateY(15px); }
    to { opacity: 1; transform: translateY(0); }
}

.animate-fade-in {
    animation: fadeIn 0.5s cubic-bezier(0.4, 0, 0.2, 1) forwards;
}

/* Gradientes de Fondo para dar Profundidad */
body::before {
    content: "";
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: radial-gradient(circle at 50% 0%, rgba(59, 130, 246, 0.08) 0%, transparent 50%),
                radial-gradient(circle at 100% 100%, rgba(244, 63, 94, 0.03) 0%, transparent 40%);
    pointer-events: none;
    z-index: -1;
}

/* Inputs con estilo Terminal/Enterprise */
.input-glass {
    background: rgba(0, 0, 0, 0.3);
    border: 1px solid var(--glass-border);
    border-radius: 1rem;
    padding: 1rem;
    color: white;
    transition: all 0.3s ease;
}

.input-glass:focus {
    outline: none;
    border-color: var(--enterprise);
    background: rgba(59, 130, 246, 0.05);
    box-shadow: 0 0 15px rgba(59, 130, 246, 0.2);
}

/* Botones con respuesta táctil */
.btn-primary {
    background: var(--enterprise);
    color: white;
    font-weight: 800;
    text-transform: uppercase;
    letter-spacing: 0.1em;
    padding: 1rem;
    border-radius: 1rem;
    transition: transform 0.1s active;
    text-align: center;
}

.btn-primary:active {
    transform: scale(0.96);
    filter: brightness(1.2);
}

/* Scrollbar invisible para estética limpia */
::-webkit-scrollbar {
    width: 0px;
    background: transparent;
}
