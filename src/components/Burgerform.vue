<template>
  <div class="container">
    <Mensagem :msg="msg" v-show="msg" />
    <div>
      <form id="burger-form" @submit="createBurger">
        
        <div class="input-container nome">
          <label for="nome">Nome do cliente: </label>
          <input type="text" id="nome" name="nome" v-model="nome" placeholder="Digite seu nome...">
        </div>

        <div class="input-container">
          <label for="pao">Escolha o pão: </label>
          <select name="pao" id="pao" v-model="pao">
            <option value="">Selecione o seu pão</option>
            <option v-for="pao in paes" :key="pao.id" :value="pao.tipo">{{ pao.tipo }}</option>
          </select>
        </div>

        <div class="input-container">
          <label for="carne">Escolha a carne do seu burger: </label>
          <select name="carne" id="carne" v-model="carne">
            <option value="">Selecione o tipo de carne</option>
            <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo">{{ carne.tipo }}</option>
          </select>
        </div>

        <div id="opcionais-container" class="input-container">
          <label id="opcionais-title" for="opcionais">Selecione os opcionais: </label>
          <div class="checkbox-container" v-for="opcional in opcionaisdata" :key="opcional.id">
            <input type="checkbox" name="opcionais" v-model="opcionais" :value="opcional.tipo"> <span>{{ opcional.tipo }}</span>
          </div>
        </div>

        <div class="input-container">
          <input type="submit" class="submit-btn" value="Criar meu Burger">
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import Mensagem from './Mensagem.vue';
  export default {
    name: "Burgerform",
    data() {
        return {
            paes: null,
            carnes: null,
            opcionaisdata: null,
            nome: null,
            pao: null,
            carne: null,
            opcionais: [],
            status: "Solicitado",
            msg: null
        };
    },
    methods: {
        async getIngredientes() {
            const req = await fetch("http://localhost:3000/ingredientes");
            const data = await req.json();
            this.paes = data.paes;
            this.carnes = data.carnes;
            this.opcionaisdata = data.opcionais;
            console.log(this.paes);
        },
        async createBurger(e) {
            e.preventDefault();
            const data = {
                nome: this.nome,
                carne: this.carne,
                pao: this.pao,
                opcionais: Array.from(this.opcionais),
                status: "Solicitado"
            };
            const dataJson = JSON.stringify(data);
            const req = await fetch("http://localhost:3000/burgers", {
                method: "POST",
                headers: { "content-Type": "application/json" },
                body: dataJson
            });
            const res = await req.json();
            // colocar mensagem de sistema
            this.msg = `Pedido Nº ${res.id} realizado com sucesso!`

            // limpar msg
            setTimeout(() => this.msg = "", 3000)
            
            // limpar os campos
            this.nome = "";
            this.pao = "";
            this.carne = "";
            this.opcionais = "";
        }
    },
    mounted() {
        this.getIngredientes();
    },
    components: { Mensagem }
}
</script>

<style scoped>
  .container {
    border-left: 2px solid #fcba03;
    border-top: 2px solid #fcba03;
    max-width: 450px;
    margin: 0 auto;
    padding: 10px;
    border-radius: 15px;
    box-shadow: 4px 4px 8px #fcba0388;
  }

  #burger-form {
    max-width: 400px;
    margin: 0 auto;
  }

  .input-container {
    display: flex;
    flex-direction: column;
    margin-bottom: 20px;
  }

  label {
    font-weight: bold;
    margin-bottom: 15px;
    color: #222;
    padding: 5px 10px;
    border-left: 4px solid #fcba03;
  }

  input, select {
    padding: 5px 10px;
    width: 300px;
  }

  #opcionais-container {
    flex-direction: row;
    flex-wrap: wrap;
  }

  #opcionais-title {
    width: 100%;
  }

  .checkbox-container {
    display: flex;
    align-items: flex-start;
    width: 50%;
    margin-bottom: 20px;
  }

  .checkbox-container span, .checkbox-container input {
    width: auto;
  }

  .checkbox-container span {
    margin-left: 6px;
    font-weight: bold;
  }

  .submit-btn {
    background-color: #222;
    color: #fcba03;
    font-weight: bold;
    border: 2px solid #fcba03;
    padding: 10px;
    font-size: 16px;
    margin: 0 auto;
    cursor: pointer;
    transition: .5s;
    width: 60%;
  }

  .submit-btn:hover {
    background-color: transparent;
    color: #222;
  }

  .input-container select {
    border: 1px solid #fcba03;
    background-color: #222;
    color: #fcba03;
    width: 100%;
  }

  .nome input {
    border: 1px solid #fcba03;
    background-color: #222;
    color: #fcba03;
    width: 100%;
  }
</style>