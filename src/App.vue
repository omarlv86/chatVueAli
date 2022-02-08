<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-logo-dark.png"
          transition="scale-transition"
          width="40"
        />

        <v-img
          alt="Vuetify Name"
          class="shrink mt-1 hidden-sm-and-down"
          contain
          min-width="100"
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-name-dark.png"
          width="100"
        />
      </div>

      <v-spacer></v-spacer>

      <v-btn
        href="https://github.com/vuetifyjs/vuetify/releases/latest"
        target="_blank"
        text
      >
        <span class="mr-2">Latest Release</span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn>
    </v-app-bar>

    <v-main>
      <!-- <HelloWorld/> -->
      <v-row justify="center" class="ma-2">
        <v-col cols="6" >
          <v-row >
            <v-col cols="12" style="border: solid 1px gray; background-color:pink">
              <v-row >
                <v-col cols="8">
                  <h3>Titulo del formulario</h3>
                  </v-col>
                <v-col cols="4">
                  <v-icon
                    x-large
                    color="white"
                  >
                    mdi-clipboard
                  </v-icon>
                </v-col>
              </v-row>
              <v-row style="padding:10px" align="center" justify="left">
                <v-icon
                    large
                    color="gray"
                    style="margin-right:10px"
                  >
                    mdi-clock
                  </v-icon>
                  En menos de 5 minutos
              </v-row>
              
            </v-col>
          </v-row>
          <v-row>
            <v-col cols="4">
              <v-img
                lazy-src="https://picsum.photos/id/11/10/6"
                max-height="150"
                max-width="250"
                src="https://picsum.photos/510/300"
                class="rounded-lg"
              ></v-img>
            </v-col>
            <v-col cols="8">
              <NombreComponente :nombreVisible.sync="nombreVisible" v-if="nombreVisible" />
              <NacimientoComponente v-if="nacimientoVisible"  :nacimientoVisible.sync="nacimientoVisible" :datosVisible.sync="datosVisible"/>
              <DatosComponente v-if="datosVisible" :datosVisible.sync="datosVisible" />
            </v-col>
          </v-row>
        </v-col>
      </v-row>
      
      
    </v-main>
  </v-app>
</template>

<script>
//import HelloWorld from './components/HelloWorld';
import NombreComponente from './components/NombreComponent.vue'
import NacimientoComponente from './components/NacimientoComponent.vue'
import DatosComponente from './components/DatosComponent.vue'

export default {
  name: 'App',

  components: {
    //HelloWorld,
    NombreComponente,
    NacimientoComponente,
    DatosComponente
  },

  data: () => ({
    //
    nombreVisible: true,
    nacimientoVisible: false,
    datosVisible: false,
  }),
  updated() {
    //console.log('nombrevisible =>',this.nombreVisible)
    console.log('nacimientoVisible =>',this.nacimientoVisible)
  },

 watch: {
      nombreVisible () {
        console.log('nombre visible =>', this.nombreVisible)
        console.log('nacimientoVisible =>',this.nacimientoVisible)
        this.nombreVisible = false;
        this.nacimientoVisible = true;
      },
      
      
    }, 

};
</script>
