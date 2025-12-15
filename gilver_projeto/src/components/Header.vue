<template>
    <header>
        <div class="logo">
            <h1>Logo aqui</h1>
        </div>
        <div class="linkagem">
            <a href="#" class="links">Home</a>
            <a href="#" class="links">Sobre</a>
            <a href="#" class="links">Musicas</a>
            <a href="#" class="links">Vídeos</a>
            <a href="#" class="links">Agenda</a>
            <a href="#" class="links">Contato</a>
        </div>
    </header>
</template>

<script>
    export default{
        name:'Header'
    }
</script>

<style>
header{
    height: 15vh;
    box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.2); /* Ajustei o box-shadow para ser menos exagerado */
    display: flex;
    flex-direction: row;
    align-items: center;
    /* CHAVE: Posiciona os itens nas extremidades (logo à esquerda, links à direita) */
    justify-content: space-between; 
    padding: 0 20px; /* Adiciona um pequeno padding nas laterais da header */
}

.linkagem{
    display: flex;
    /* CHAVE: Remove o posicionamento absoluto que estava causando o problema */
    /* position: absolute; */ 
    /* left: 1; */
    gap: 20px;
    margin-right: 15vh;
}

.links{
    text-decoration: none;
    color: #333; /* Adicionado uma cor inicial para o texto */
    transition: .5s;
    padding: 10px;
    border-radius: 10px;
}

.links:hover{
    text-decoration: none;
    padding: 10px;
    color: white;
    background-color: rgb(48, 48, 240);
    border-radius: 10px;
}

.logo{
    background-color: gray;
    width: 70px; /* Ajustado para um valor fixo mais comum */
    height: 70px; /* Ajustado para um valor fixo mais comum */
    display: flex; /* Adicionado para centralizar o '.' */
    justify-content: center;
    align-items: center;
    border-radius: 10px;
    margin-left: 20vh;
} 

.logo h1 {
    color: white;
    margin: 0;
}
</style>