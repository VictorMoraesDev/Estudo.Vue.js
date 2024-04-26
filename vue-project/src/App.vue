<script setup>
import {reactive} from 'vue';

  const nome = "gian souza"
  const meuObj = {
    nome: "gian",
    filmeFavorito: "Rocky"
  }

    function dizOla(nome) {
      return `${nome} diz oi`;
    }

const enderecoDaImagemDoBatman = "https://wallup.net/wp-content/uploads/2016/01/220756-Batman-Batman_Arkham_Knight.jpg";
const imagemDoSuperman ="https://th.bing.com/th/id/OIP.Et3U6Hu_9o_UvCDp951ruAHaEo?rs=1&pid=ImgDetMain";

const botaoEstaDesabilitado = false

const gostaDoBatman = false
const gostaDoSuperman = false

const estaAutorizado = false

// let contador = 0
const estado = reactive({
  contador: 0,
  email:'',
  saldo: 5000,
  Transferindo: 0,
  nomes: ['gian', 'paulo', 'luisa', 'monica'],
  nomeAInserir: '',
})

function incrementar() {
  estado.contador++;
}

function decrementar() {
  estado.contador--;
}

function alteraEmail(evento) {
 estado.email = evento.target.value;
}

function mostraSaldoFuturo() {
  const { saldo, Transferindo } = estado;
  return saldo - Transferindo;
}

function validaValorTransferencia() {
  const { saldo, Transferindo } = estado;
  return saldo => Transferindo;
}

function cadastrarNome() {
  if (estado.nomeAInserir.length >= 3) {
    estado.nomes.push(estado.nomeAInserir)
  } else {
    alert("Digite mais caracteres")
  }
}


</script>

<template>
  <h1>{{ dizOla("paula") }}</h1>
  <img v-if="gostaDoBatman" :src="enderecoDaImagemDoBatman" alt="">
  <img v-else-if="gostaDoSuperman" :src="imagemDoSuperman" alt="">
  <h2 v-else>Não curte heróis da DC</h2>

  <h1 v-if="estaAutorizado">Bem-vindo</h1>
  <h1 v-else>Não possui acesso</h1>
 

  <button :disabled="botaoEstaDesabilitado">Enviar mensagem</button>

  <br />
  <hr />

  {{ estado.contador }}

<button @click="incrementar" type="button">+</button>
<button @click="decrementar" type="button">-</button>

<br />
<hr />

{{ estado.email }}
<input type="email" @keyup="alteraEmail">

<br />
<hr />

Saldo: {{ estado.saldo }} <br />
Transferindo: {{ estado.Transferindo }} <br />
Saldo depois da trânsferencia: {{ mostraSaldoFuturo() }} <br />
<input class="campo" :class="{invalido: !validaValorTransferencia()}" @keyup="evento => estado.Transferindo = evento.target.value" type="number" placeholder="Quantia para transferir " />
<button v-if="validaValorTransferencia()">Transferir</button>
<span v-else>Valor muito maior que o saldo</span>

<br />
<hr />

<ul>
  <li v-for="nome in estado.nomes">
    {{ nome }}
  </li>
</ul>
<input @keyup="evento => estado.NomeAInserir = evento.target.value" type="text" placeholder="Digite um novo nome">
<button @click="cadastrarNome" type="button">Cadastrar nome</button>

<h3 v-for="nome in estado.nomes">{{ nome }}</h3>
</template>

<style scoped>

img {
  max-width: 200px;
}

.invalido {
  outline-color:red ;
  border-color: red;
}

.campo {
  border: 2px solid #000;
}

</style>
