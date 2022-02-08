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
                <h3>¿Cual es tu fecha de nacimiento?</h3>
        <v-card-text>

          <v-text-field
            ref="dia"
            v-model="dia"
            :rules="diaRules"
            :error-messages="errorMessages"
            type="number"
            label="Dia"
            required
          ></v-text-field>

          <v-select
            :items="meses"
            label="Mes"
            ref="mes"
            v-model="mes"
            :rules="[() => !!mes || 'Este campo es requerido']"
          ></v-select>

          <v-text-field
            ref="año"
            v-model="año"
            :rules="añoRules"
            :error-messages="errorMessages"
            label="Año"
            required
          ></v-text-field>

          <v-row v-if="show">
            <v-col cols="12"
                sm="12"
                md="12"
                lg="12"
                style="background-color:pink"
                >
                <p>{{ dia }} {{ mes }} {{ año }}</p>
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
        nacimientoVisible: Boolean,
        datosVisible: Boolean
    },
    data: () => ({
      errorMessages: '',
      dia: null,
      mes:null,
      meses: ['Enero','Febrero','Marzo', 'Abril','Mayo','Junio','Julio','Agosto','Septiembre','Octubre','Noviembre','Diciembre'],
      año: null,
      apellidoMaterno: null,
      formHasErrors: false,
      show: false,
      diaRules: [
        v => !!v || "Este campo es requerido", 
        v => v > 0 || 'El valor debe ser mayor a cero',
        v => v < 32 || 'el dia maximo es 31'
      ],
      añoRules: [
        v => !!v || "Este campo es requerido", 
        v => v > 1960 || 'El año minimo es 1960',
        v => v <= 2015 || 'El año maximo es 2015'
      ],
    }),
    
    computed: {
      form () {
        return {
          dia: this.dia,
          mes: this.mes,
          año: this.año,
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
            const fecha = `${this.dia} ${this.mes} ${this.año}`  
            localStorage.setItem("fecha", fecha);
            setTimeout(() => {
                this.$emit('update:nacimientoVisible', !this.nacimientoVisible);
                this.$emit('update:datosVisible', !this.datosVisible);
                this.show = false;
            }, 3000);
        }
      },
    },
  }
</script>

<style>

</style>