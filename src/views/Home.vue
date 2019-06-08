<template>
  <div class="home">
    <!-- linka valores html com js -->
    <h2>V-BIND:</h2>
    <span v-bind:title="titulo">{{texto}}</span>
    <br>
    
    <!-- Condicional (destroi e constroi) -->
    <h2>V-IF/ELSE:</h2>
    <div v-if="true">
      V-IF
    </div>
    <div v-else>
      V-ELSE
    </div>
    <br>
    
    <!-- mostra e esconde -->
    <h2>V-SHOW:</h2>
    <div v-show="false">
      V-SHOW
    </div>

    <!-- estrutura de repetição -->
    <h2>V-FOR:</h2>
    <ul>
     <li v-for="item in lista">
       {{ item.nome }}
     </li>
    </ul>
    <br>

    <!-- escuta eventos -->
    <h2>V-ON:</h2>
    <button v-on:click="$_console">CONSOLE</button>
    <br>

    <!-- TWO WAY BIND -->
    <h2>V-MODEL:</h2>
    <input v-model="mensagem"/>
    <p>{{ mensagem }}</p>
    <button v-on:click="$_console">CONSOLE</button>
    <br>

    <!-- guarda valores em cache -->
    <h2>COMPUTED</h2>
    <!-- <p> {{inverterMensagemComputed}} </p>
    <p> {{$_inverterMensagemMethod()}} </p>
    <p> {{numero1}} </p>
    <p> {{numero2}} </p> -->
    <br>

    <!-- observador de valores -->
    <h2>WATCH</h2>
    <p> {{contadorAlteracoes}} </p>
    <br>
    
    <h2>ACESSO API</h2>
    <div >
      <p>
        Faça uma pergunta do tipo sim/não:
        <input v-model="pergunta">
      </p>
    <p>{{ resposta }}</p>
    <button v-on:click="getResposta()">Perguntar</button>
    </div>

  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'home',
  components: {
    // HelloWorld
  },

  data () {
    return {
      titulo: 'titulo teste',

      texto: 'ola pessoal',

      lista: [
        { nome: '1' },
        { nome: '2' },
        { nome: 'teste' }
      ],

      numero1: 0,

      numero2: 0,

      contadorAlteracoes: 0,

      mensagem: '',

      pergunta: '',

      resposta: 'Eu não posso responder até que você faça uma pergunta!'
    }
  },

  computed: {
    inverterMensagemComputed () {
      // this.numero1++
      return this.texto.split('').reverse().join('')
    }
  },

  watch: {
    mensagem: function () {
      this.contadorAlteracoes++
    }
  },

  methods: {
    $_inverterMensagemMethod () {
      this.numero2++
      return this.texto.split('').reverse().join('')
    },

    $_console () {
      // V-ON
      // console.log(this.numero1)
      // console.log(this.numero2)
      
      // V-MODEL
      //console.log(this.mensagem)
    },

    getResposta () {
      if (this.pergunta.indexOf('?') === -1) {
        this.resposta = 'Perguntas geralmente têm uma interrogação. ;-)'
        return
      }
      this.resposta = 'Pensando...'
      this.$axios.get('https://yesno.wtf/api')
        .then((response) => {
          this.resposta = response.data.answer === 'yes' ? 'Sim.' : response.data.answer === 'no' ? 'Não.' : 'Talvez!'
        })
        .catch((error) => {
          this.resposta = 'Erro! Não pode executar a API. ' + error
        })
    }
  }
}
</script>
