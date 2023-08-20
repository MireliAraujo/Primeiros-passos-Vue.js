<script setup>
import { reactive } from 'vue';
const nome ="mireli"
const meuObg = {
    nome: "mrieli",
    filmFavorit: "duro de matar"
}

function dizOla(nome) {
    return `${nome} diz oi` ;
}

const fotoCaptaMatvel = "https://th.bing.com/th/id/OIP.wRlJcNlseX8Ob7zRSk2CsgHaHa?pid=ImgDet&rs=1"
const fotoMMaravilha = "https://th.bing.com/th/id/OIP.oJ5ZaN2_p9Qr3iuRhnhP8gHaEo?pid=ImgDet&rs=1"

const botaoDesab = false

const gostaDaMarvel = false
const gostaDaMMaravilha = false
const estaAutorizado = false

//let contador = 0

const estado = reactive({
    contador: 0,
    email: '',
    saldo: 5000,
    transferindo: 0,
    nomes:  ['gian', 'paulo', 'luiz', 'monica'],
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
    const { saldo, transferindo } = estado;
    return saldo - transferindo;
}

function validaValorTransferencia() {
    const { saldo, transferindo } = estado;
    return saldo >= transferindo;
}


function cadastrarnome(){
    if(estado.nomeAInserir.length >= 3){
        estado.nomes.push(estado.nomeAInserir)
    } else{
        alert("digite mais caracteries")
    }
}


</script>


<template>
    
        <h1>{{ dizOla("paula") }}</h1>
    <img v-if="gostaDaMarvel" :src="fotoCaptaMatvel">
    <img v-else-if="gostaDaMMaravilha" :src="fotoMMaravilha">
    <h2 v-else>Não curte heróis</h2>

    <h1 v-if="estaAutorizado">Bem vindo</h1>
    <h1 v-else>Não possue acesso</h1>

    <button :disabled="!botaoDesab">enviar msg</button>
    <br>
    <hr>

    {{ estado.contador }}

    <button @click="incrementar" type="button">+</button>
    <button @click="decrementar" type="button">-</button>

    <br>
    <hr>

    {{  estado.email }}
    <input type="email" @keyup="alteraEmail">

    <br>
    <hr>

    Saldo: {{ estado.saldo }} <br>
    Transferindo: {{ estado.transferindo }} <br>
    Saldo depois da transferência: {{ mostraSaldoFuturo() }} <br>
    <input :class="{ invalido: !validaValorTransferencia() }" @keyup="evento => estado.transferindo = evento.target.value" type="number" placeholder="Quantia transferência" >
    <button v-if="validaValorTransferencia()">Transferir</button>
    <span v-else>Valor maior que o saldo</span>

    <br>
    <hr>


    

    <ul>
        <li v-for="nome in estado.nomes">
            {{ nome }}
        </li>
    </ul>
    <input @keyup='evento => estado.nomeAInserir = evento.target.value' type="text" placeholder="digite um novo nome">
    <button @click="cadastrarnome" type="button">Cadastrar</button>

</template>

<style scoped>

img{
    max-width: 200px;
}

.invalido {
    outline-color: red;
    border-color: red;
}

</style>
