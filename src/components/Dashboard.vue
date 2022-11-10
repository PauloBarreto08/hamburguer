<template>
  <div>
    
    <div>

    <table class="w-[1200px] m-auto table-fixed">
  <thead>
    <tr class="border-b-2  border-black">
      <th class="w-[60px] text-left">#:</th>
      <th class="text-left">Cliente:</th>
      <th class="text-left">Pão:</th>
      <th class="text-left">Carne:</th>
      <th class="text-left">Opcionais:</th>
      <th class="w-[260px] h-[50px] text-left">Ações:</th>
    </tr>
  </thead>
  <tbody v-if="burgers" class="">
    <tr class="border-top border-b-2" v-for="burger in burgers" :key="burger.id">
      <td>{{ burger.id }}</td>
      <td>{{ burger.nome }}</td>
      <td>{{ burger.pao }}</td>
      <td>{{ burger.carne }}</td>
      <td>
        <div v-for="(opcional, index) in burger.opcionais" :key="index">
              <li>{{ opcional }}</li>
        </div>
      </td>
      <td class="w-[1px] text-left">
        <select name="status" class=" p-[15px]" @change="updateBurger($event, burger.id)">
              <option class="pr-[15px]" :value="s.tipo" v-for="s in status" :key="s.id" :selected="burger.status == s.tipo">
                {{ s.tipo }}
              </option>
        </select>
        <button class="m-[10px] delete-btn bg-stone-900 hover:bg-yellow-500 text-yellow-500 hover:text-black font-bold p-[10px]" @click="deleteBurger(burger.id)">Cancelar</button>
      </td>
    </tr>
  </tbody>
  <div v-else class="w-[1160px] m-5 border-b-2">
    <h2 class="text-center mb-5">Não há pedidos no momento!</h2>
  </div>
      </table>

    </div>


    </div>  
  </template>
  <script>
    export default {
      name: "Dashboard",
      data() {
        return {
          burgers: null,
          burger_id: null,
          status: []
        }
      },
      methods: {
        async getPedidos() {
          const req = await fetch('http://localhost:3000/burgers')
          const data = await req.json()
          this.burgers = data
          // Resgata os status de pedidos
          this.getStatus()
        },
        async getStatus() {
          const req = await fetch('http://localhost:3000/status')
          const data = await req.json()
          this.status = data
        },
        async deleteBurger(id) {
          const req = await fetch(`http://localhost:3000/burgers/${id}`, {
            method: "DELETE"
          });
          const res = await req.json()
          console.log(res)
          this.getPedidos()
        },
        async updateBurger(event, id) {
          const option = event.target.value;
          const dataJson = JSON.stringify({status: option});
          const req = await fetch(`http://localhost:3000/burgers/${id}`, {
            method: "PATCH",
            headers: { "Content-Type" : "application/json" },
            body: dataJson
          });
          const res = await req.json()
          console.log(res)
        }
      },
      mounted () {
      this.getPedidos()
      }
    }
  </script>
  
  <style scoped>
  </style>