<template>
  <Toaster position="top-right" richColors />
  <v-row justify="center">
    <v-col cols="12" lg="6" md="8" sm="10">
      <v-form ref="form">
        <v-card class="mx-auto my-8" elevation="16">
          <v-card-item>
            <v-card-title>
              Crear nueva tarifa
            </v-card-title>
          </v-card-item>

          <v-card-text>
            <v-text-field label="#ID Tarifa" variant="outlined" v-model="tarifa.idTarifa" :rules="rules" required>
            </v-text-field>
            <v-text-field label="Tarifa" variant="outlined" v-model="tarifa.tarifa" :rules="rules" required>
            </v-text-field>
            <v-text-field label="Concepto" variant="outlined" v-model="tarifa.concepto" :rules="rules" required>
            </v-text-field>
            <v-text-field label="Tipo de Producto" variant="outlined" v-model="tarifa.tipoProducto" :rules="rules"
              required>
            </v-text-field>
            <v-date-input label="Dia inicio" variant="outlined" prepend-icon="" v-model="tarifa.diaInicio" required
              :rules="rules"></v-date-input>
            <v-date-input label="Dia Fin" variant="outlined" prepend-icon="" v-model="tarifa.diaFin" required
              :rules="rules"></v-date-input>
            <v-text-field label="Importe" variant="outlined" :model-value="tarifa.importe" prefix="$" :rules="rules"
              required>
            </v-text-field>
          </v-card-text>
          <v-card-actions>
            <v-btn variant="text" to="/">
              Cancelar
            </v-btn>
            <v-spacer></v-spacer>
            <v-slide-x-reverse-transition>
              <v-tooltip v-if="formHasErrors" location="left">
                <template v-slot:activator="{ on, attrs }">
                  <v-btn class="my-0" icon v-bind="attrs" v-on="on" @click="resetForm">
                    <v-icon>mdi-refresh</v-icon>
                  </v-btn>
                </template>
                <span>Refresh form</span>
              </v-tooltip>
            </v-slide-x-reverse-transition>
            <v-btn color="primary" variant="text" @click="submit">
              Crear
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-form>
    </v-col>
  </v-row>
</template>

<script>
import { VDateInput } from 'vuetify/labs/VDateInput'
import { Toaster, toast } from 'vue-sonner'

export default {
  components: {
    VDateInput,
    Toaster
  },
  data() {
    return {
      tarifa: {
        idTarifa: '',
        tarifa: '',
        concepto: '',
        estatus: '',
        tipoProducto: '',
        tipoDocumento: '',
        diaInicio: null,
        diaFin: null,
        importe: 0,
        fh_ultima_modificacion: '',
        aplicativos: [],
      },
      rules: [
        value => {
          if (value) return true
          return 'Este campo es requerido.'
        },
      ],
      formHasErrors: false,
    }
  },
  methods: {
    resetForm() {
      this.formHasErrors = false
      this.$refs.form.reset()
    },
    async submit() {
      const { valid } = await this.$refs.form.validate()

      if (valid) {
        // Obtenemos las tarifas existentes del localStorage
        const tarifasExistentes = JSON.parse(localStorage.getItem('tarifas')) || [];

        // Agregamos la nueva tarifa al array
        tarifasExistentes.push(this.tarifa);

        // Guardamos el array actualizado en localStorage
        localStorage.setItem('tarifas', JSON.stringify(tarifasExistentes));
        toast.success('Tarifa creada exitosamente');
        this.resetForm();
      } else {
        this.formHasErrors = true
        toast.warning('Por favor, revisa los campos del formulario');
      }
    }
  }
}

</script>
