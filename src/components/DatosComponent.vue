<template>
  <v-container>
     <v-row>
         <v-col
          cols="12"
          sm="12"
          md="12"
          lg="12"
         >
            <v-card ref="form">
              <h3>Datos de contacto</h3>
        <v-card-text>

          <v-text-field
            ref="correo"
            v-model="correo"
            :rules="emailRules"
            :error-messages="errorMessages"
            type="email"
            label="Correo electronico"
            required
          ></v-text-field>

          <v-text-field
            ref="telefono"
            v-model="telefono"
            :rules="phoneRules"
            :error-messages="errorMessages"
            type="tel"
            label="Telefono"
            required
          ></v-text-field>

          <v-row v-if="show">
            <v-col cols="12"
                sm="12"
                md="12"
                lg="12"
                style="background-color:pink"
                >
                <p>correo electronico: {{ correo }}</p>
                <p>telefono: {{ telefono }}</p>
            </v-col>
          </v-row>
          <v-row v-if="showDataValid">
       <v-col
         cols="12"
         sm="12"
         md="12"
         lg="12"
       >
        <p>Si tus datos son correctos, por favor continuemos</p>
       </v-col>
      <v-col
         cols="12"
         sm="12"
         md="12"
         lg="12"
         style="text-align:center"
       >
        <v-btn
            depressed
            color="pink"
            text
            @click="iniciar"
          >
            Iniciar
          </v-btn>
       </v-col>
     </v-row>

      <v-row v-if="endData">
       <v-col
         cols="12"
         sm="12"
         md="12"
         lg="12"
         style="background-color:pink"
       >
        <p>Fecha de nacimiento: {{ fechaForm }}</p>
        <p>Correo electronico: {{ correo }} </p>
        <p>Telefono celular: {{ telefono }}</p>
        <p>Nombre: {{ nombreForm }} {{ apellidoForm }} </p>
       </v-col>
     </v-row>

        </v-card-text>
        <v-divider class="mt-12"></v-divider>
        <v-card-actions style="justify-content:center" v-if="showBtn">
          <v-btn
            icon
            color="primary"
            text
            @click="submit"
          >
            Enviar
            <v-icon
        large
      >
        mdi-chevron-right
      </v-icon>
          </v-btn>
        </v-card-actions>
      </v-card>
         </v-col>
     </v-row>
     

     

  
  </v-container>
</template>

<script>
export default {
    props:{
        datosVisible: Boolean,
    },
    data: () => ({
      errorMessages: '',
      correo: null,
      telefono:null,
      showDataValid:false,
      endData:false,
      show: false,
      showBtn: true,

      nombreForm: '',
      apellidoForm:'',
      fechaForm:'',
      emailRules: [
        v => !!v || 'E-mail es requerido',
        v => /.+@.+/.test(v) || 'E-mail must be valid',
      ],
      phoneRules: [
        v => !!v || 'El Telefono es requerido',
        v => (v && v.length <= 10) || 'El telefono tiene 10 digitos',
      ],
    }),
    
    computed: {
      form () {
        return {
          correo: this.correo,
          telefono: this.telefono,
        }
      },
    },

    watch: {
      dia () {
        this.errorMessages = ''
      },
    },

    methods: {
      submit () {
        this.formHasErrors = false

        Object.keys(this.form).forEach(f => {
          if (!this.form[f]) this.formHasErrors = true

          this.$refs[f].validate(true)
        })

        if(this.formHasErrors == false){
            this.show = true;
            this.showDataValid = true;

            localStorage.setItem("correo", this.correo);
            localStorage.setItem("telefono", this.telefono);
            this.showBtn = false;
        }
      },

      iniciar(){

        this.nombreForm = localStorage.getItem('nombre');
        this.apellidoForm = localStorage.getItem('apellidop');
        this.fechaForm = localStorage.getItem('fecha');

        this.endData = true;
        
      }
    },
  }
</script>

<style>

</style>