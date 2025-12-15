<template>
    <div id="duda-ascensao-site">
        <i class="bi bi-list menu-hamburguer" @click="toggleSidebar"></i>

        <div :class="['sidebar', { 'aberto': sidebarAberto }]">
            <button class="fechar-sidebar" @click="toggleSidebar">✕</button>
            <nav class="menu-navegacao">
                <a href="#inicio" @click="toggleSidebar">Início</a>
                <a href="#biografia" @click="toggleSidebar">Biografia</a>
                <a href="#projetos" @click="toggleSidebar">Projetos</a>
                <a href="#" @click.prevent="abrirModal">Discografia</a>
            </nav>
        </div>

        <section class="inicio" id="inicio">
            <div class="conteiner fade-in">
                <h1 class="slogan slide-up">Pagode que o povo canta!!</h1>
                <h2 class="sub-slogan slide-up delay-1">O novo álbum já está disponível. Ouça agora!</h2>
                
                <div class="botoes slide-up delay-2">
                    <a class="links primary-btn" id="ouca-btn" href="#" @click.prevent="toggleStreaming">Ouça agora</a>
                    <a class="links secondary-btn" id="agendar-btn" href="#">Agendar Show</a> 
                </div>

                <div :class="['streaming-links', { 'aberto': streamingAberto }]">
                    <a href="https://www.youtube.com/@DudaAscensao" target="_blank" class="link-plataforma slide-in-bottom">
                        <img src="../assets/img/logo-youtube.png" alt="YouTube Music">
                    </a>
                    <a href="https://www.deezer.com/br/artist/292700761?host=375222457&utm_campaign=clipboard-generic&utm_source=user_sharing&utm_content=artist-292700761&deferredFl=1&fbclid=PAVERFWAOnfXJleHRuA2FlbQIxMQBzcnRjBmFwcF9pZA8xMjQwMjQ1NzQyODc0MTQAAaecoMw4AQFPFGUDMyhjUboNeI7IlS14Kx_E2FJa-j9DXmLmOR7nzcR1kD0xoA_aem_Z7I1C2RAaptoLNeOnO-MgA"
                        target="_blank" class="link-plataforma slide-in-bottom delay-1">
                        <img src="../assets/img/logo-deezer.png" alt="Deezer">
                    </a>
                    <a href="https://open.spotify.com/intl-pt/artist/6NGnG8vvHMH5OZOGmmwQts" target="_blank"
                        class="link-plataforma slide-in-bottom delay-2">
                        <img src="../assets/img/logo-spotify.png" alt="Spotify">
                    </a>
                </div>
            </div>
        </section>

        <section class="bio-section" id="biografia">
            <div class="conteudo">
                <div class="conteiner-img fade-in-left">
                    <img class="img-cantando" src="../assets/img/img-gilver/imagem-cantando.jpg"
                        alt="Gilver Ascensão cantando com microfone">
                </div>

                <div class="apresentacao">
                    <div class="title-ele slide-in-right">
                        <div class="icone-anos">
                            <p>10 anos de pagode</p>
                        </div>
                        <h1 class="title">Duda Ascensão</h1>
                    </div>

                    <div class="biografia">
                        <p class="bio-paragraph slide-up delay-1">
                            A jornada de <strong>Duda Ascensão</strong> no pagode começou cedo,
                            inspirada pelas rodas de samba.
                        </p>
                        <p class="bio-paragraph slide-up delay-2">
                            Sua música conecta tradição e modernidade, levando o
                            <strong>Pagode que o Povo Canta</strong> a todos os públicos.
                        </p>
                    </div>

                    <div class="btns-biografia slide-up delay-3">
                        <button id="btn-discos" @click="abrirModal">Discografia</button>
                        <a id="btn-contratar" href="#">Contrate / Orçamento</a>
                    </div>
                </div>
            </div>
        </section>

        <transition name="modal-fade">
            <div class="modal-overlay" v-if="modalAberto" @click.self="fecharModal">
                <div class="modal-discos fade-in-scale">
                    <button class="fechar-modal" @click="fecharModal">✕</button>
                    <h2 class="titulo-discos">Discografia</h2>
                    <div class="grid-discos scroll-custom">
                        <div class="card-disco slide-up-item" v-for="i in 10" :key="i">
                            <img :src="`../assets/img/discos/disco${i}.png`" :alt="`Capa do Disco ${i}`">
                            <div class="info-disco">
                                <h3>Título do Disco {{ i }}</h3>
                                <span>{{ ['Single', 'EP', 'Álbum'][i % 3] }} • 202{{ 9 - i % 4 }}</span>
                                <a target="_blank" :href="`http://googleusercontent.com/spotify.com/${i}`" class="btn-disco">Ouvir agora</a>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </transition>

        <section class="projetos" id="projetos" :class="[currentProject.fundoClass]">
            
            <div class="seletor-container slide-in-right">
                <h2>Projetos em Destaque</h2>
                <select v-model="projetoSelecionado" class="seletor-projeto">
                    <option value="projeto1">Projeto 1: Pagode que o povo canta</option>
                    <option value="projeto2">Projeto 2: Hoje tem amor</option>
                    <option value="projeto3">Projeto 3: Novo Lançamento</option>
                </select>
            </div>

            <div class="apresentacao-projeto fade-in-scale-content">
                <h3 class="titulo-projeto">{{ currentProject.titulo }}</h3>
                <p class="descricao-projeto">{{ currentProject.descricao }}</p>
                
                <button @click="toggleMidia" class="btn-midia-toggle">
                    {{ midiaVisivel ? 'Ocultar Mídia' : 'Ver Vídeos / Fotos' }}
                </button>

                <div :class="['container-midia', { 'midia-aberta': midiaVisivel }]" v-html="currentProject.htmlMidia">
                    </div>
            </div>
        </section>

        <Footer />
    </div>
</template>
<script>
import Footer from './Footer.vue' // Assumindo que o componente Footer existe

// Importe os assets aqui (os caminhos relativos ao arquivo .vue)
// NOTA: No código real, esses arquivos devem existir no caminho especificado (ex: src/assets/img/video/video-apresentação.mp4)
import videoProjeto1 from '../assets/img/video/video-apresentação.mp4'; 
import imagemProjeto2 from '../assets/img/img-gilver/imagem-cantando.jpg'; 

// Definição dos dados dos projetos
const DADOS_PROJETOS = {
    projeto1: {
        fundoClass: 'fundo-projeto-1',
        titulo: 'Pagode que o povo canta',
        descricao: 'O show de lançamento do álbum "Pagode que o Povo Canta" trouxe a essência do samba para o palco, apresentando faixas inéditas e clássicos do gênero.',
        htmlMidia: `
            <video controls src="${videoProjeto1}" class="midia-projeto" poster="../assets/img/fundos/fundo-disco-section.jpg" preload="none"></video>
        `
    },
    projeto2: {
        fundoClass: 'fundo-projeto-2',
        titulo: 'Hoje Tem Amor',
        descricao: 'Uma homenagem ao pagode romântico, o projeto "Hoje Tem Amor" de 2019 apresenta canções de tirar o fôlego e letras profundas.',
        htmlMidia: `
            <img src="${imagemProjeto2}" alt="Duda Ascensão em performance" class="midia-projeto img-projeto">
        `
    },
    projeto3: {
        fundoClass: 'fundo-projeto-3',
        titulo: 'Em Breve: Novo Lançamento!',
        descricao: 'Fique ligado para o nosso próximo projeto, com grandes surpresas e a essência do nosso pagode. Novo álbum a caminho!',
        htmlMidia: `
            <p class="midia-placeholder">Conteúdo de Mídia indisponível no momento.</p>
        `
    }
};

export default {
    name: 'Index',
    components: { Footer },
    data() {
        return {
            modalAberto: false,
            streamingAberto: false,
            projetoSelecionado: 'projeto1',
            dadosProjetos: DADOS_PROJETOS,
            sidebarAberto: false,
            // Estado para controlar a exibição da mídia do projeto
            midiaVisivel: false 
        }
    },
    computed: {
        currentProject() {
            return this.dadosProjetos[this.projetoSelecionado];
        }
    },
    watch: {
        // Reseta a visibilidade da mídia toda vez que o projeto muda
        projetoSelecionado() {
            this.midiaVisivel = false;
        }
    },
    methods: {
        abrirModal() {
            this.modalAberto = true
            document.body.style.overflow = 'hidden' // Desabilita o scroll do body
            if (this.sidebarAberto) {
                this.toggleSidebar();
            }
        },
        fecharModal() {
            this.modalAberto = false
            document.body.style.overflow = 'auto' // Reabilita o scroll do body
        },
        toggleStreaming() {
            this.streamingAberto = !this.streamingAberto;
        },
        toggleSidebar() {
            this.sidebarAberto = !this.sidebarAberto;
            document.body.style.overflow = this.sidebarAberto || this.modalAberto ? 'hidden' : 'auto';
        },
        toggleMidia() {
            this.midiaVisivel = !this.midiaVisivel;
        }
    }
}

</script>
<style>
/* --------------------------------------
   PALETA DE CORES (Baseada em Pagode/Samba)
   - Fundo: #0A0A0A (Quase preto)
   - Destaque 1: #FFC800 (Amarelo Ouro/Limão)
   - Destaque 2: #FF8C00 (Laranja Vibrante)
   - Texto: #FFFFFF (Branco)
-------------------------------------- */

/* 0. Configurações Globais */
:root {
    --color-bg: #0A0A0A;
    --color-primary: #FFC800; /* Amarelo */
    --color-secondary: #FF8C00; /* Laranja */
    --color-text-light: #FFFFFF;
    --color-text-dark: #1A1A1A;
    --spacing-lg: 3rem;
    --spacing-md: 1.5rem;
    --transition-duration: 0.4s;
}

body {
    margin: 0;
    padding: 0;
    font-family: 'Poppins', sans-serif; /* Fonte moderna e legível */
    background-color: var(--color-bg);
    color: var(--color-text-light);
    transition: overflow var(--transition-duration); 
}

/* --------------------------------------
   1. SEÇÃO INÍCIO (HERO)
-------------------------------------- */
.inicio {
    height: 100vh;
    min-height: 600px;
    /* Fundo com gradiente escuro para realçar o texto */
    background-image: linear-gradient(120deg, rgba(10, 10, 10, 0.95), rgba(10, 10, 10, 0.5)), 
                      url(../assets/img/fundos/fundo-disco-section.jpg);
    background-repeat: no-repeat;
    background-size: cover;
    background-position: center center;
    display: flex;
    align-items: center;
    justify-content: center; /* Centralizado ou alinhado à esquerda em telas grandes */
    padding: 0 5%;
    box-shadow: inset 0 -10px 20px rgba(0, 0, 0, 0.5); /* Sombra interna sutil */
}

.conteiner {
    max-width: 700px;
    width: 100%;
    position: relative;
    display: flex;
    flex-direction: column;
    gap: var(--spacing-md);
    text-align: left;
}

@media (min-width: 1200px) {
    .conteiner {
        /* Empurra o conteúdo para o centro/lado direito em telas grandes */
        margin-left: 50vw; 
        transform: translateX(-50%);
    }
}

/* Tipografia Refinada */
.slogan {
    color: var(--color-primary);
    font-size: clamp(3rem, 7vw, 5.5rem);
    font-weight: 900;
    line-height: 1.1;
    margin: 0;
    text-shadow: 0 0 15px rgba(255, 200, 0, 0.5);
}

.sub-slogan {
    font-size: clamp(1.2rem, 2.5vw, 1.8rem);
    font-weight: 400;
    margin: 0;
    color: var(--color-text-light);
}

/* 2. BOTÕES (INÍCIO) */
.botoes {
    display: flex;
    flex-direction: row;
    gap: var(--spacing-md);
    margin-top: var(--spacing-lg);
}

.links {
    text-decoration: none;
    font-weight: 700;
    text-transform: uppercase;
    padding: 1rem 2.5rem;
    border-radius: 50px; /* Botões arredondados modernos */
    transition: all var(--transition-duration) ease;
    font-size: 1rem;
    border: 2px solid;
    white-space: nowrap;
    text-align: center;
    flex-grow: 1;
    max-width: 250px;
}

.primary-btn {
    background-color: var(--color-secondary);
    color: var(--color-text-dark);
    border-color: var(--color-secondary);
    box-shadow: 0 5px 15px rgba(255, 140, 0, 0.4);
}

.primary-btn:hover {
    background-color: var(--color-primary);
    border-color: var(--color-primary);
    color: var(--color-text-dark);
    transform: translateY(-3px);
    box-shadow: 0 8px 20px rgba(255, 200, 0, 0.6);
}

.secondary-btn {
    background-color: transparent;
    color: var(--color-primary);
    border-color: var(--color-primary);
}

.secondary-btn:hover {
    background-color: var(--color-primary);
    color: var(--color-text-dark);
    border-color: var(--color-primary);
    transform: translateY(-3px);
}

/* 3. GAVETA DE STREAMING (Animação de gaveta) */
.streaming-links {
    display: flex;
    flex-direction: row;
    gap: var(--spacing-md);
    max-height: 0;
    overflow: hidden;
    transition: max-height 0.6s ease-in-out, margin-top 0.6s ease-in-out;
    padding: 0 0; 
    margin-top: 0;
}

.streaming-links.aberto {
    max-height: 100px;
    margin-top: var(--spacing-md);
}

.link-plataforma {
    display: block;
    width: 60px;
    height: 60px;
    border-radius: 50%;
    background-color: rgba(255, 255, 255, 0.1);
    box-shadow: 0 0 10px rgba(255, 255, 255, 0.1);
    transition: transform 0.3s ease, box-shadow 0.3s ease;
    padding: 10px;
}

.link-plataforma:hover {
    transform: scale(1.15);
    box-shadow: 0 0 25px var(--color-primary);
}

.link-plataforma img {
    width: 100%;
    height: 100%;
    object-fit: contain; /* Para que os logos sejam exibidos corretamente */
}

/* --------------------------------------
   4. SEÇÃO BIOGRAFIA
-------------------------------------- */
.bio-section {
    padding: 100px 5%;
    background-color: var(--color-bg);
    color: var(--color-text-light);
    border-top: 1px solid rgba(255, 255, 255, 0.05);
}

.conteudo {
    display: flex;
    max-width: 1200px;
    margin: 0 auto;
    align-items: center;
    gap: 80px; /* Espaçamento maior entre imagem e texto */
}

/* 4.1. Imagem */
.conteiner-img {
    flex-shrink: 0;
    box-shadow: 0 10px 30px rgba(255, 200, 0, 0.4);
    border-radius: 15px; /* Bordas ligeiramente mais suaves */
    overflow: hidden;
    transition: transform 0.4s ease-out;
    border: 4px solid var(--color-primary);
}

.conteiner-img:hover {
    transform: scale(1.05);
}

.img-cantando {
    width: 400px; /* Tamanho maior para impacto */
    height: 400px;
    object-fit: cover;
    display: block;
}

/* 4.2. Área de Apresentação (Texto) */
.apresentacao {
    flex-grow: 1;
}

.title-ele {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    gap: 15px;
}

.icone-anos {
    background: linear-gradient(90deg, var(--color-primary), var(--color-secondary));
    color: var(--color-text-dark);
    padding: 8px 20px;
    border-radius: 50px;
    font-weight: 800;
    text-transform: uppercase;
}

.title {
    font-size: clamp(3rem, 6vw, 5rem);
    font-weight: 900;
    color: var(--color-primary);
    margin: 0 0 20px 0;
}

.biografia p {
    font-weight: 300;
    font-size: 1.2rem;
    line-height: 1.7;
    margin-bottom: var(--spacing-md);
}

.biografia strong {
    color: var(--color-primary);
    font-weight: 700;
}

/* 4.3. Botões de Biografia */
.btns-biografia {
    display: flex;
    flex-direction: row;
    gap: 20px;
    margin-top: 40px;
}

#btn-discos, #btn-contratar {
    font-size: 1rem;
    padding: 14px 30px;
    border-radius: 50px;
    text-transform: uppercase;
    font-weight: 700;
    transition: all var(--transition-duration) ease;
    border: 2px solid;
    cursor: pointer;
}

#btn-discos {
    background: var(--color-primary);
    color: var(--color-text-dark);
    border-color: var(--color-primary);
    text-decoration: none;
}

#btn-discos:hover {
    background: transparent;
    color: var(--color-primary);
    box-shadow: 0 0 10px var(--color-primary);
    transform: translateY(-3px);
}

#btn-contratar {
    background: transparent;
    color: var(--color-text-light);
    border-color: var(--color-text-light);
    text-decoration: none;
}

#btn-contratar:hover {
    background: var(--color-text-light);
    color: var(--color-text-dark);
    transform: translateY(-3px);
}


/* --------------------------------------
   5. ANIMAÇÕES GERAIS (Scroll Reveal Like)
   (Serão ativadas quando o elemento for visível)
-------------------------------------- */

.fade-in { opacity: 0; animation: fadeIn 1s ease-out forwards; }
.slide-up { opacity: 0; transform: translateY(20px); animation: slideUp 1s ease-out forwards; }
.slide-in-left { opacity: 0; transform: translateX(-30px); animation: slideInLeft 1s ease-out forwards; }
.slide-in-right { opacity: 0; transform: translateX(30px); animation: slideInRight 1s ease-out forwards; }
.slide-in-bottom { opacity: 0; transform: translateY(10px); animation: slideUp 0.6s ease-out forwards; }

@keyframes fadeIn { to { opacity: 1; } }
@keyframes slideUp { to { opacity: 1; transform: translateY(0); } }
@keyframes slideInLeft { to { opacity: 1; transform: translateX(0); } }
@keyframes slideInRight { to { opacity: 1; transform: translateX(0); } }

.delay-1 { animation-delay: 0.2s; }
.delay-2 { animation-delay: 0.4s; }
.delay-3 { animation-delay: 0.6s; }


/* --------------------------------------
   6. MODAL DE DISCOGRAFIA (Animações de entrada/saída)
-------------------------------------- */
.modal-overlay {
    position: fixed;
    inset: 0;
    background: rgba(0, 0, 0, .95);
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 9999; /* Z-index alto */
    opacity: 1;
}

/* Animações de transição do Vue para o Overlay */
.modal-fade-enter-active, .modal-fade-leave-active {
  transition: opacity 0.4s ease;
}
.modal-fade-enter, .modal-fade-leave-to {
  opacity: 0;
}

.modal-discos {
    background: linear-gradient(120deg, var(--color-bg), rgba(10, 10, 10, 0.8));
    width: 90%;
    max-width: 1200px;
    max-height: 90vh;
    padding: 50px;
    border-radius: 20px;
    position: relative;
    color: var(--color-text-light); 
    border: 1px solid rgba(255, 255, 255, 0.1);
    box-shadow: 0 10px 40px rgba(0, 0, 0, 0.8);
    /* Animação de entrada do Modal em si */
    transform: scale(1);
    opacity: 1;
}

.modal-fade-enter-active .modal-discos, .modal-fade-leave-active .modal-discos {
    transition: transform 0.4s cubic-bezier(0.25, 0.8, 0.25, 1), opacity 0.4s ease;
}
.modal-fade-enter .modal-discos, .modal-fade-leave-to .modal-discos {
    transform: scale(0.95);
    opacity: 0;
}

.titulo-discos {
    font-size: 3rem;
    color: var(--color-primary);
    margin-top: 0;
    margin-bottom: 40px;
    text-align: center;
}

.fechar-modal {
    position: absolute;
    top: 25px;
    right: 30px;
    font-size: 2.5rem;
    background: none;
    border: none;
    cursor: pointer;
    color: var(--color-text-light);
    transition: color 0.3s, transform 0.3s;
}
.fechar-modal:hover {
    color: var(--color-secondary);
    transform: rotate(90deg);
}

.grid-discos {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); /* Layout flexível e moderno */
    gap: 30px;
    max-height: 60vh;
    overflow-y: auto;
    padding-right: 15px;
}

.card-disco {
    background: #1A1A1A;
    border-radius: 10px;
    overflow: hidden;
    display: flex;
    flex-direction: column;
    box-shadow: 0 5px 20px rgba(0, 0, 0, 0.3);
    transition: transform 0.3s ease, box-shadow 0.3s ease;
}
.card-disco:hover {
    transform: translateY(-5px);
    box-shadow: 0 10px 30px rgba(255, 200, 0, 0.2);
}

.card-disco img {
    width: 100%;
    aspect-ratio: 1/1; /* Capa quadrada */
    object-fit: cover;
    transition: transform 0.5s;
}
.card-disco:hover img {
    transform: scale(1.05);
}

.info-disco {
    padding: 15px;
    display: flex;
    flex-direction: column;
    flex: 1;
    text-align: center;
}
.info-disco h3 { color: var(--color-primary); margin: 0 0 5px 0; }
.info-disco span { font-size: 0.9rem; color: #BBB; margin-bottom: 15px; }


.btn-disco {
    margin-top: auto;
    align-self: stretch;
    padding: 10px;
    background: var(--color-secondary);
    color: var(--color-text-dark);
    border-radius: 50px;
    font-weight: 700;
    text-decoration: none;
    transition: background 0.3s, transform 0.3s;
}

.btn-disco:hover {
    background: var(--color-primary);
    transform: translateY(-2px);
}

/* Estilos da barra de rolagem (mantidos e melhorados) */
.scroll-custom::-webkit-scrollbar { width: 10px; }
.scroll-custom::-webkit-scrollbar-track { background: rgba(255, 255, 255, 0.05); border-radius: 10px; }
.scroll-custom::-webkit-scrollbar-thumb { background: linear-gradient(180deg, var(--color-secondary), var(--color-primary)); border-radius: 10px; }
.scroll-custom::-webkit-scrollbar-thumb:hover { background: var(--color-secondary); }


/* --------------------------------------
   7. SEÇÃO PROJETOS (Modern Background Switch)
-------------------------------------- */
.projetos {
    min-height: 80vh;
    background-repeat: no-repeat;
    background-size: cover;
    background-position: center;
    /* Transição suave de fundo */
    transition: background-image 1s ease-in-out; 
    padding: 80px 5%;
    position: relative; 
    display: flex;
    flex-direction: column;
    align-items: center;
}

/* Fundos (Otimizados para ter gradiente escuro) */
.projetos::before {
    content: '';
    position: absolute;
    inset: 0;
    background: rgba(0, 0, 0, 0.6);
    z-index: 1;
    transition: background 1s;
}
.fundo-projeto-1 { background-image: url(../assets/img/fundos/fundo-disco-section.jpg); }
.fundo-projeto-2 { background-image: url(../assets/img/fundos/Inicial-gilver.jpg); }
.fundo-projeto-3 { background-image: url(../assets/img/fundos/fundo-escuro.jpg); }


/* Container do Seletor */
.seletor-container {
    background-color: rgba(10, 10, 10, 0.95);
    color: var(--color-text-light);
    padding: 25px 35px;
    border-radius: 15px;
    text-align: center;
    box-shadow: 0 5px 20px rgba(0, 0, 0, 0.7);
    border: 2px solid var(--color-primary);
    
    position: absolute;
    top: 50px;
    right: 5%;
    max-width: 350px;
    width: 90%; 
    z-index: 10;
}
.seletor-container h2 {
    margin-top: 0;
    font-size: 1.6rem;
    color: var(--color-primary);
}

.seletor-projeto {
    padding: 12px 20px;
    font-size: 1.1rem;
    border-radius: 8px;
    border: 2px solid var(--color-secondary);
    background-color: var(--color-bg);
    color: var(--color-text-light);
    cursor: pointer;
    margin-top: 15px;
    width: 100%;
    transition: border-color 0.3s;
}
.seletor-projeto:focus {
    outline: none;
    border-color: var(--color-primary);
    box-shadow: 0 0 10px rgba(255, 200, 0, 0.5);
}


/* CONTAINER PRINCIPAL DE APRESENTAÇÃO */
.apresentacao-projeto {
    background-color: rgba(10, 10, 10, 0.9);
    color: var(--color-text-light);
    padding: 50px;
    border-radius: 20px;
    max-width: 800px;
    width: 90%;
    text-align: center;
    box-shadow: 0 0 40px rgba(255, 140, 0, 0.6);
    margin-top: 100px; 
    z-index: 5; /* Acima do fundo */
    transition: opacity 0.5s, transform 0.5s;
}

.titulo-projeto {
    font-size: clamp(2rem, 4vw, 3.5rem);
    color: var(--color-secondary);
    margin-top: 0;
}

.descricao-projeto {
    font-size: 1.2rem;
    line-height: 1.7;
    margin-bottom: 30px;
    color: #EEE;
}

/* Botão de Toggle da Mídia */
.btn-midia-toggle {
    background-color: var(--color-primary);
    color: var(--color-text-dark);
    border: none;
    padding: 14px 35px;
    border-radius: 50px;
    font-weight: 700;
    text-transform: uppercase;
    cursor: pointer;
    transition: all 0.3s ease;
    margin-bottom: 25px;
    box-shadow: 0 3px 10px rgba(0, 0, 0, 0.3);
}

.btn-midia-toggle:hover {
    background-color: var(--color-secondary);
    color: var(--color-text-light);
    transform: translateY(-2px);
}

/* CONTAINER DE MÍDIA (Gaveta Animada) */
.container-midia {
    max-height: 0;
    overflow: hidden;
    padding: 0;
    transition: max-height 1s cubic-bezier(0.23, 1, 0.32, 1), padding 1s ease-in-out;
    border-top: 2px solid transparent;
    margin-top: 0;
}

.container-midia.midia-aberta {
    max-height: 1000px; /* Valor grande para garantir que caiba */
    padding: 30px 0;
    border-top: 2px solid rgba(255, 255, 255, 0.1);
    margin-top: 20px;
}

.midia-projeto {
    width: 100%;
    max-width: 700px;
    border-radius: 15px;
    display: block;
    margin: 0 auto;
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.7);
    height: auto;
}

.img-projeto {
    max-height: 500px;
    object-fit: contain;
}

.midia-placeholder {
    color: #666;
    font-style: italic;
    font-size: 1.1rem;
}


/* --------------------------------------
   8. SIDEBAR (Menu Lateral)
-------------------------------------- */
.sidebar {
    position: fixed;
    top: 0;
    right: 0;
    z-index: 9990; /* Abaixo do modal, mas acima de tudo o resto */
    width: 300px;
    height: 100%;
    background: rgba(10, 10, 10, 0.98);
    backdrop-filter: blur(10px);
    box-shadow: -10px 0 20px rgba(0, 0, 0, 0.8);
    transform: translateX(100%);
    transition: transform 0.5s cubic-bezier(0.25, 0.8, 0.25, 1);
    padding: 30px;
    display: flex;
    flex-direction: column;
}

.sidebar.aberto {
    transform: translateX(0);
}

.fechar-sidebar {
    background: none;
    border: none;
    color: var(--color-primary);
    font-size: 3rem;
    align-self: flex-end;
    cursor: pointer;
    padding: 0 10px;
    margin-bottom: 40px;
    transition: color 0.3s;
}
.fechar-sidebar:hover {
    color: var(--color-secondary);
}

.menu-navegacao {
    display: flex;
    flex-direction: column;
    gap: 15px;
}

.menu-navegacao a {
    color: var(--color-text-light);
    text-decoration: none;
    font-size: 1.8rem;
    font-weight: 700;
    padding: 10px 10px;
    transition: all 0.3s ease;
    border-left: 5px solid transparent;
}

.menu-navegacao a:hover {
    color: var(--color-primary);
    padding-left: 20px;
    border-left: 5px solid var(--color-primary);
    background: rgba(255, 200, 0, 0.1);
}

.menu-hamburguer {
    z-index: 9991; 
    cursor: pointer;
    color: var(--color-primary);
    position: fixed;
    top: 30px;
    right: 30px;
    font-size: 40px;
    transition: .3s;
    background: rgba(10, 10, 10, 0.5);
    border-radius: 50%;
    padding: 5px 10px;
    box-shadow: 0 0 15px rgba(255, 200, 0, 0.5);
}

.menu-hamburguer:hover {
    color: var(--color-secondary);
    transform: scale(1.1);
}


/* --------------------------------------
   9. RESPONSIVIDADE (Ajustes Finais)
-------------------------------------- */
@media (max-width: 1200px) {
    .conteudo {
        gap: 40px;
    }
    .img-cantando { width: 350px; height: 350px; }
}

@media (max-width: 992px) {
    .conteudo {
        flex-direction: column;
        text-align: center;
        gap: 50px;
    }
    .conteiner-img { border-width: 2px; }
    .title-ele { align-items: center; }
    .btns-biografia { justify-content: center; }
    .apresentacao { padding: 0 20px; }

    .seletor-container {
        position: static; 
        margin: 0 auto 50px auto; 
        width: 100%;
        max-width: 90%;
        top: auto;
        right: auto;
    }
    .apresentacao-projeto {
        margin-top: 0;
    }
    .projetos { padding-top: 50px; }
}

@media (max-width: 768px) {
    .inicio { justify-content: flex-end; align-items: flex-start; padding-top: 100px; }
    .conteiner { margin: 0; text-align: center; }
    .slogan, .sub-slogan { text-align: center; }
    .botoes { flex-direction: column; align-items: center; }
    .links { width: 90%; max-width: 350px; }
    .streaming-links { justify-content: center; }
}

@media (max-width: 600px) {
    .img-cantando { width: 280px; height: 280px; }
    .btns-biografia { flex-direction: column; }
    #btn-discos, #btn-contratar { max-width: 100%; }
    .modal-discos { padding: 25px; }
    .grid-discos { gap: 20px; }
}
</style>