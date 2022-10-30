<template>

  <section class="src-componentes-http-client">
    <div class="jumbotron">
      <h2>Componente HttpClient</h2>
      <hr>
      <hr>
      <br>

      <button class="btn btn-warning my-3 mr-3" @click="getUsuariosXHRCb()">Pedir XHR</button>      
      <button class="btn btn-info my-3 mr-3" @click="getUsuariosFetch()">Pedir Fetch</button>
      <button class="btn btn-success my-3 mr-3" @click="getUsuariosAxios()">Pedir Axios</button>


      <button class="btn btn-danger my-3 mr-3" @click="usuarios = []">Clear</button>
      <br>

      <div v-if="usuarios.length" class="table-responsive">
        <table class="table table-dark">
          <tr>
            <th>Nombre</th>
            <th>Email</th>
            <th>NroTelefono</th>
          </tr>
          <tr v-for="usuario in usuarios" :key="usuario.id">
            <td>{{ usuario.nombre }}</td>
            <td>{{ usuario.email }}</td>
            <td>{{ usuario.nroTelefono }}</td>
          </tr>
        </table>
      </div>
      <h4 v-else class="alert alert-danger text-center">No se encuentran datos</h4>
      
    </div>
  </section>

</template>

<script>

  export default  {
    name: 'src-componentes-http-client',
    props: [],
    mounted () {

    },
    data () {
      return {
        url:  'https://635e2037ed25a0b5fe3f0be1.mockapi.io/usuarios',
        usuarios : []
      }
    },
    methods: {
      getUsuariosXHRCb() {
        const xhr = new XMLHttpRequest()
        xhr.open('get', this.url)
        xhr.addEventListener('load', () => {
          if(xhr.status == 200) {
            let respuesta = JSON.parse(xhr.response)
            this.usuarios = respuesta
          }
        })
        xhr.send()
      },
      async getUsuariosFetch() {
        try {
          let response = await fetch(this.url)
          console.log(response)
          let respuesta = await response.json()
          this.usuarios = respuesta
        }
        catch(error) {
          console.error(error)
        }
      },
      async getUsuariosAxios() {
        try {
          let respuesta = await this.axios(this.url)
          this.usuarios = respuesta.data
        }
        catch(error) { console.error(error) } 

      }

    },
    computed: {

    }
}


</script>

<style scoped lang="css">
  .src-componentes-http-client {

  }

  .jumbotron {
    background-color: teal;
    color: white;
  }

  hr {
    background-color: #bbb;
  }

</style>
