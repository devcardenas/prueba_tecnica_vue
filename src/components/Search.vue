<template>
  <Toaster position="top-right" richColors />
  <div>
    <v-card class="mx-auto my-8" elevation="16">
      <v-card-item>
        <v-card-title>
          Buscar por #ID
        </v-card-title>
      </v-card-item>

      <v-card-text>
        <div class="d-flex align-center">
          <v-text-field label="" variant="outlined" v-model="idTarifa" @keyup.enter="search"
            placeholder="Escribe el #ID y presiona ENTER">
            <v-icon>
              mdi-magnify
            </v-icon>
          </v-text-field>
        </div>
        <v-divider></v-divider>
        <Results :results="results" :loading="loading" />
      </v-card-text>
    </v-card>
  </div>
</template>

<script>
import Results from '../components/Results.vue'
import { Toaster, toast } from 'vue-sonner'

export default {
  components: {
    Results,
    Toaster
  },
  data() {
    return {
      loading: false,
      idTarifa: null,
      results: []
    };
  },
  methods: {
    async search() {
      this.loading = true;
      this.results = await this.searchInAPI();
      this.results = await this.searchInLocal();
      this.loading = false;
      if (!this.results) {
        toast.error('No se encontraron resultados');
      }
    },
    async searchInAPI() {
      try {
        const response = await fetch(`https://ebind-dev.egl-cloud.com/dgs-api-bridge/tarifas/consulta`, {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json',
          },
          body: JSON.stringify({ idTarifa: this.idTarifa }),
        });
        const data = await response.json();
        return data.response.tarifas;
      } catch (error) {
        toast.error('Ocurrió un error al buscar la tarifa en el servidor');
        return [];
      }
    },
    searchInLocal() {
      const tarifas = JSON.parse(localStorage.getItem('tarifas')) || [];
      return tarifas.filter(tarifa => tarifa.idTarifa === this.idTarifa);
    }
  }
}
</script>