<template>
    <footer>
        <div class="footer-content">
            <div class="footer-section about">
                <h2>Ascenção</h2>
                <p>slogan a definir</p>
            </div>

            <div class="footer-section links">
                <h3>Atalhos</h3>
                <ul>
                    <li><a href="#">Início</a></li>
                    <li><a href="#">Política de Privacidade</a></li>
                    <li><a href="#">Autor</a></li>
                    <li><a href="#">Suporte</a></li>
                </ul>
            </div>

            <div class="footer-section social">
                <h3>Conecte-se</h3>
                <div class="social-icons">
                    <a target="_blank" rel="noopener noreferrer" href="https://www.facebook.com/joao.gabriel.715685"><i
                            class="bi bi-facebook"></i></a>
                    <a target="_blank" rel="noopener noreferrer" href="https://www.instagram.com/jaomtz_09/"><i class="bi bi-instagram"></i></a>
                    <a target="_blank" rel="noopener noreferrer" href="https://www.linkedin.com/in/jo%C3%A3o-gabriel-506031260/"><i
                            class="bi bi-linkedin"></i></a>
                    <a target="_blank" rel="noopener noreferrer" href="https://x.com/home"><i class="bi bi-twitter-x"></i></a> 
                    <a target="_blank" rel="noopener noreferrer" href="https://github.com/Joaogb00"><i class="bi bi-github"></i></a>
                </div>
            </div>
        </div>
        
       

        <div class="footer-bottom">
            <p>© 2025 Ascenção — Todos os direitos reservados.</p>
        </div>
    </footer>
</template>

<script>
export default {
    name: 'Footer'
}
</script>

<style scoped>
/* Cor primária: #00b3d6 */
/* Cor de fundo: rgb(0, 20, 25) */

footer {
    background: linear-gradient(180deg, rgb(0, 20, 25), black);
    color: white;
    /* Ajustado o padding para 40px no topo/fundo e 60px nas laterais */
    padding: 40px 60px 20px; 
    box-shadow: inset 2px 0px 2px 0px rgb(0, 20, 25);
    border-top: 10px solid rgb(0, 20, 25);
    font-family: 'Poppins', sans-serif;
}

.footer-content {
    display: flex;
    justify-content: space-around; /* Usei space-around para melhor espaçamento inicial */
    flex-wrap: wrap;
    gap: 40px;
    margin-bottom: 30px; /* Adiciona margem entre o conteúdo principal e a seção Parceiros */
}

.footer-section h2,
.footer-section h3 {
    color: #00b3d6;
    margin-bottom: 10px;
}

.footer-section p {
    max-width: 300px;
    line-height: 1.5;
    font-size: 0.95rem; /* Ajuste sutil no tamanho da fonte */
}

.footer-section ul {
    list-style: none;
    padding: 0;
}

.footer-section ul li {
    margin-bottom: 5px; /* Adicionado um pequeno espaçamento entre os links */
}

.footer-section ul li a {
    color: #d4d4d4;
    text-decoration: none;
    transition: color 0.3s ease; /* Mais detalhado */
}

.footer-section ul li a:hover {
    color: #00b3d6;
}

.social-icons a {
    color: white;
    margin-right: 15px; /* Um pouco mais de espaço */
    font-size: 1.5rem; /* Levemente maior */
    transition: color 0.3s ease;
}

.social-icons a:hover {
    color: #00b3d6;
}

/* ESTILOS DA SEÇÃO DE PARCEIROS */
#parceiros {
    text-align: center;
    padding: 20px 0;
    border-top: 1px solid #0a3a44; /* Linha de separação */
}

.parceiros-title {
    color: #00b3d6;
    margin-bottom: 25px;
    font-size: 1.8rem;
}

.logos {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-wrap: wrap;
    gap: 30px;
    padding: 10px 0;
}

.logos img {
    max-height: 60px; /* Altura máxima para as logos */
   
    opacity: 0.7;
    transition: filter 0.3s ease, opacity 0.3s ease;
}

.logos a:hover img {
    filter: none; /* Remove o filtro ao passar o mouse */
    opacity: 1;
}

/* FIM DOS ESTILOS DE PARCEIROS */


.footer-bottom {
    text-align: center;
    margin-top: 30px; /* Aumentei a margem para separar melhor */
    border-top: 1px solid #0a3a44;
    padding-top: 15px; /* Aumentei o padding */
    font-size: 0.9rem;
    color: #aaa;
}

/* Responsividade para telas menores */
@media (max-width: 768px) {
    footer {
        padding: 30px 20px 15px;
    }

    .footer-content {
        justify-content: flex-start;
        flex-direction: column;
        gap: 30px;
    }

    .footer-section {
        width: 100%;
    }

    .logos {
        gap: 20px;
    }

    .logos img {
        max-height: 30px;
    }
}
</style>