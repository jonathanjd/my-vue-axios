<template>
    <v-app>
        <v-container grid-list-xs>
            <v-layout row wrap>
                <v-flex xs12>
                    <v-card>
                        <v-card-media height="300" src="/img/card-app-media.jpeg">
                        </v-card-media>
                        <v-card-title primary-title>
                            <div>
                                <h1>App Axios</h1>
                            </div>
                        </v-card-title>
                        <v-container grid-list-xs>
                            <v-layout row wrap>
                                <v-flex xs6>
                                    <h3 class="text-md-center">Listar Mensaje</h3>
                                    <v-list>
                                        <v-list-tile avatar v-for="(mensaje, index) in getMensajes" :key="index">
                                            <v-list-tile-action>
                                                <v-icon color="red">mail</v-icon>
                                            </v-list-tile-action>
                                            <v-list-tile-content>
                                                {{ mensaje }}
                                            </v-list-tile-content>
                                        </v-list-tile>
                                    </v-list>
                                </v-flex>
                                <v-flex xs6>
                                    <h3 class="text-md-center">Crear Mensaje</h3>
                                    <v-form>
                                        <v-text-field name="mensaje" label="Mensaje:" v-model="inputMensaje" multi-line></v-text-field>
                                        <v-btn :disabled="validarButton" color="primary" @click="guardar">Guardar</v-btn>
                                        <v-btn @click="limpiarInput">Limpiar</v-btn>
                                    </v-form>
                                </v-flex>
                            </v-layout>
                        </v-container>
                        <v-snackbar :timeout="timeout" :color="color" :multi-line="mode === 'multi-line'" :vertical="mode === 'vertical'" v-model="snackbar">
                            {{ textSucces }}
                            <v-btn dark flat @click.native="snackbar = false">Close</v-btn>
                        </v-snackbar>
                    </v-card>
                </v-flex>
            </v-layout>
        </v-container>
    </v-app>
</template>

<script>
export default {
  data() {
    return {
      snackbar: false,
      color: 'success',
      mode: '',
      timeout: 6000,
      textSucces: 'Mensaje Registrado',
      inputMensaje: '',
      mensajes: ['Mensaje 123456', 'Mensaje 987654', 'Mensaje 987455']
    };
  },
  computed: {
    getMensajes() {
      return this.mensajes;
    },
    validarButton() {
      return this.inputMensaje == '';
    }
  },
  methods: {
    guardar() {
      this.mensajes.push(this.inputMensaje);
      this.snackbar = true;
      this.limpiarInput();
    },

    limpiarInput() {
      this.inputMensaje = '';
    }
  }
};
</script>

<style>
</style>
