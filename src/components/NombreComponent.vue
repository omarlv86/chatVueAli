<template>
  <v-container>
      <v-row justify="center">
    <v-col
      cols="12"
      sm="12"
      md="12"
      lg="12"
    >
      <v-card ref="form">
        <h3>¿Cual es tu nombre?</h3>
        <v-card-text>
          <v-text-field
            ref="nombre"
            v-model="nombre"
            :rules="[() => !!nombre || 'Este campo es requerido']"
            :error-messages="errorMessages"
            label="Nombre"
            required
          ></v-text-field>
          <v-text-field
            ref="segundoNombre"
            v-model="segundoNombre"
            :rules="[() => !!segundoNombre || 'Este campo es requerido']"
            :error-messages="errorMessages"
            label="Segundo nombre"
            required
          ></v-text-field>

          <v-text-field
            ref="apellidoPaterno"
            v-model="apellidoPaterno"
            :rules="[() => !!apellidoPaterno || 'Este campo es requerido']"
            :error-messages="errorMessages"
            label="Apellido paterno"
            required
          ></v-text-field>

          <v-text-field
            ref="apellidoMaterno"
            v-model="apellidoMaterno"
            :rules="[() => !!apellidoMaterno || 'Este campo es requerido']"
            :error-messages="errorMessages"
            label="Apellido Materno"
            required
          ></v-text-field>

          <v-row v-if="show">
            <v-col cols="12"
                sm="12"
                md="12"
                lg="12"
                style="background-color:pink"
                >
                <p>{{ nombre }} {{ segundoNombre }}</p>
            </v-col>
          </v-row>
        </v-card-text>
        <v-divider class="mt-12"></v-divider>
        <v-card-actions style="justify-content:center">
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
        nombreVisible: Boolean,
    },
    data: () => ({
      errorMessages: '',
      nombre: null,
      segundoNombre: null,
      apellidoPaterno: null,
      apellidoMaterno: null,
      formHasErrors: false,
      show: false
    }),
    
    computed: {
      form () {
        return {
          nombre: this.nombre,
          segundoNombre: this.segundoNombre,
          apellidoPaterno: this.apellidoPaterno,
          apellidoMaterno: this.apellidoMaterno,
        }
      },
    },

    watch: {
      nombre () {
        this.errorMessages = ''
      },
    },

    methods: {
      addressCheck () {
        this.errorMessages = this.address && !this.nombre
          ? `Hey! I'm required`
          : ''

        return true
      },
      resetForm () {
        this.errorMessages = []
        this.formHasErrors = false

        Object.keys(this.form).forEach(f => {
          this.$refs[f].reset()
        })
      },
      submit () {
        this.formHasErrors = false

        Object.keys(this.form).forEach(f => {
          if (!this.form[f]) this.formHasErrors = true

          this.$refs[f].validate(true)
        })

        if(this.formHasErrors == false){
            this.show = true;
            localStorage.setItem("nombre", this.nombre);
            localStorage.setItem("apellidop", this.apellidoPaterno);
            setTimeout(() => {
                this.$emit('update:nombreVisible', !this.nombreVisible);
                this.show = false;
            }, 3000);
        }
      },
    },
  }
</script>

<style>

</style>