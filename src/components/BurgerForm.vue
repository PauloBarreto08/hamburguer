<template>
    <div>
      <Message :msg="msg" v-show="msg" />
      <div class="mt-10 flex justify-center">
      <form id="burger-form" class="max-w-md" @submit="createBurger">
          <div class="input-container flex-col flex mb-5 ">
            <div class="border-l-4 border-yellow-400 mb-4 flex items-center">
                <strong class="ml-2 " for="nome">Nome dos clientes:</strong>
            </div>
            <div>
                <input type="text" id="nome" name="nome" v-model="nome" placeholder="Digite o seu nome" class="h-30 p-1 pr-40 border">
            </div>      
          </div>

          <div class="input-container flex-col flex mb-5 ">
            <div class="border-l-4 border-yellow-400 text-start mb-4 flex items-center">
                <strong class="ml-2" for="pao">Escolha o pao:</strong>
            </div>
            <div>
                <select class="p-1 pr-[238px] w-400 border" name="pao" id="pao" v-model="pao">
                    <option>selecione o seu pao</option>
                    <option v-for="pao in paes" :key="pao.id" :value="pao.tipo">
                        {{ pao.tipo }}
                    </option>
                </select>
            </div>
             
              
          </div>
          <div class="input-container flex-col flex mb-5">
            <div class="border-l-4 border-yellow-400 mb-4 flex items-center">
                <strong class="ml-2" for="carne">Escolha a carne do seu hamburguer:</strong>
            </div>
            <div>
                <select class="p-1 pr-[265px] w-400 border" name="carne" id="carne" v-model="carne">
                    <option>selecione a carne</option>
                    <option v-for="carne in carnes" :key="carne.id" value="carne">
                        {{ carne.tipo }}
                    </option>
                </select>
            </div>
             
          
          </div>
          <div class="input-container flex-wrap flex mb-5 flex-row">
            <div class="border-l-4 border-yellow-400 mb-4  ">
            <label class="ml-2 font-bold" id="opcionais-title" for="opcionais">Selecione os opcionais</label>
            </div>
     
            <div class="w-1/2"></div>
            <div class="mb-[20px] w-1/2 items-start" v-for="opcional in opcionaisdata" :key="opcional.id">
                <input type="checkbox" name="opcionais" v-model="opcionais" :value="opcional.tipo">
                <span class="w-auto ml-[6px] font-bold">{{ opcional.tipo }}</span>
            </div>
        </div>

          <div>
              <button class="bg-stone-900 hover:bg-yellow-500 text-yellow-500 hover:text-black font-bold py-2 px-32" value="Criar meu hamburguer">Criar meu hamburguer</button>
          </div>
      </form>
    </div>
    </div>
  </template>
  
  <script>
      // import axios from "axios"
      import Message from "./Message.vue"
  
  export default {
      name: 'BurgerForm',
      data(){
          return{
              paes: null,
              carnes: null,
              opcionaisdata: null,
              nome: null,
              pao: null,
              carne: null,
              opcionais: [],
              msg: null
          }
      },
      methods:{
          async getIngredientes(){
              const req = await fetch("http://localhost:3000/ingredientes");
              const data = await req.json();
  
              this.paes = data.paes;
              this.carnes = data.carnes;
              this.opcionaisdata = data.opcionais;
          },
          async createBurger() {
             
  
              const data = {
                  nome: this.nome,
                  carne: this.carne,
                  pao: this.pao,
                  opcionais: Array.from(this.opcionais),
                  status: "solicitado"
              }
  
              const dataJson = JSON.stringify(data);
  
              const req = await fetch("http://localhost:3000/burgers", {
                  method: "POST",
                  headers: { "content-Type": "application/json" },
                  body: dataJson
              });
  
              const res = await req.json();
  
              this.msg = `Pedido num ${res.id} realizado com sucesso`;
              
               setTimeout(() => this.msg = "", 3000);
  
              this.nome = "";
              this.carne = "";
              this.pao = "";
              this.opcionais = "";
  
          //    axios.post("http://localhost:3000/burgers", data)
          //    .then((response) => {
          //     console.log(response.data)
          //     this.pedido = response.data;
  
          //     this.msg = `Pedido numero ${response.id} realizado com sucesso`
  
             
  
          //    }).catch((error) => {
          //     alert(error)
  
          //    }).finally(()=>{
          //     this.nome = "";
          //     this.carne = "";
          //     this.pao = "";
          //     this.opcionais = "";
          //    })
          },
      },
      mounted(){
          this.getIngredientes();
      },
      components:{
          Message
      },
  }
  </script>
  
  <style scoped>

  </style>