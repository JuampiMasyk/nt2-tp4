<template>

  <section class="src-componentes-formulario-av">
    <div class="jumbotron">
      <h2>Componente FormularioAv</h2>
      <hr>
      <hr>
      <br>

      <vue-form :state="formState" @submit.prevent="enviar()">

        <!-- ---------------------------------- -->
        <!--            CAMPO NOMBRE            -->
        <!-- ---------------------------------- -->
        <validate tag="div">
          <label for="nombre">Nombre</label>
          <input 
            type="text" 
            id="nombre" 
            class="form-control" 
            autocomplete="off"
            v-model.trim="formData.nombre" 
            name="nombre"
            required
            :minlength="nombreMinLength"
            :maxlength="nombreMaxLenght"
            no-espacios
          >
          <!-- mensajes de validación -->
          <field-messages name="nombre" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Campo requerido</div>
            <div slot="minlength" class="alert alert-danger mt-1">
              Este campo debe poseer al menos {{ nombreMinLength }} caracteres.
            </div>
            <div slot="maxlength" class="alert alert-danger mt-1">
              Este campo debe poseer menos de {{ nombreMaxLength }} caracteres.
            </div>
            <div slot="no-espacios" class="alert alert-danger mt-1">
              Este campo no permite espacios intermedios
            </div>

          </field-messages>
        </validate>
    
        <br>

        <!-- ---------------------------------- -->
        <!--             CAMPO EDAD             -->
        <!-- ---------------------------------- -->
        <validate tag="div">
          <label for="edad">Edad</label>
          <input 
            type="number" 
            id="edad" 
            class="form-control" 
            autocomplete="off"
            v-model.number="formData.edad" 
            name="edad"
            required
            :min="edadMin"
            :max="edadMax"
          >
          <!-- mensajes de validación -->
          <field-messages name="edad" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Campo requerido</div>
            <div slot="min" class="alert alert-danger mt-1">
              La edad mínima debe ser {{ edadMin }} años.
            </div>
            <div slot="max" class="alert alert-danger mt-1">
              La edad máxima debe ser {{ edadMax }} años.
            </div>
          </field-messages>
        </validate>

        <br>

        <!-- ---------------------------------- -->
        <!--            CAMPO EMAIL             -->
        <!-- ---------------------------------- -->
        <validate tag="div">
          <label for="email">Email</label>
          <input 
            type="email" 
            id="email" 
            class="form-control" 
            autocomplete="off"
            v-model.trim="formData.email" 
            name="email"
            required
          >
          <!-- mensajes de validación -->
          <field-messages name="email" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Campo requerido</div>
            <div slot="email" class="alert alert-danger mt-1">Email no válido</div>
          </field-messages>
        </validate>
        <br>

        <button class="btn btn-success my-3" :disabled="formState.$invalid">Enviar</button>

      </vue-form>    

      <div v-if="datos.length" class="table-responsive">
        <table class="table">
          <tr>
            <th>Nombre</th>
            <th>Edad</th>
            <th>Email</th>
          </tr>
          <tr v-for="(dato,index) in datos" :key="index">
            <td>{{ dato.nombre }}</td>
            <td>{{ dato.edad }}</td>
            <td>{{ dato.email }}</td>
          </tr>
        </table>
      </div>
      <h3 v-else class="alert alert-info">No hay gastos ingresados</h3>


    </div>
  </section>

</template>

<script>

  export default  {
    name: 'src-componentes-formulario-av',
    props: [],
    mounted () {

    },
    data () {
      return {
        formState : {},
        formData: this.getInitialData(),
        nombreMinLength: 5,
        nombreMaxLength: 15,
        edadMin: 18,
        edadMax: 120,
        datos:[],
      }
    },
    methods: {
      getInitialData() {
        return {
          nombre: null,
          edad: null,
          email: null
        }
    },
    enviar() {
      let dato = {...this.formData}

      console.log(dato)
        this.datos.push(dato)

      this.formData = this.getInitialData()
      this.formState._reset()
    }
    },
    computed: {

    }
}


</script>

<style scoped lang="css">
  .src-componentes-formulario-av {

  }

  .jumbotron {
    background-color: purple;
    color: white;
  }

  hr {
    background-color: #bbb;
  }

  pre {
    color: white;
  }
</style>