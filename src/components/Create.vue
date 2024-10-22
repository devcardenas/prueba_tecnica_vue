<template>
  <div>
    <v-card class="mx-auto my-8" elevation="16">
      <v-card-item>
        <v-card-title>
          Crear nuevo registro
        </v-card-title>
      </v-card-item>

      <v-card-text>
        <v-row>
          <v-col cols="12" lg="6">
            <v-text-field label="#ID Tarifa" variant="outlined" v-model="idTarifa">
            </v-text-field>
            <v-text-field label="Tarifa" variant="outlined" v-model="tarifa">
            </v-text-field>
            <v-text-field label="Concepto" variant="outlined" v-model="concepto">
            </v-text-field>
            <v-text-field label="Estatus" variant="outlined" v-model="estatus">
            </v-text-field>
            <v-text-field label="Tipo de Producto" variant="outlined" v-model="tipoProducto">
            </v-text-field>
            <v-text-field label="Tipo de Documento" variant="outlined" v-model="tipoDocumento">
            </v-text-field>
            <v-text-field label="Día Inicio" variant="outlined" v-model="diaInicio">
            </v-text-field>
            <v-text-field label="Día Fin" variant="outlined" v-model="diaFin">
            </v-text-field>
            <v-text-field label="Importe" variant="outlined" v-model="importe">
            </v-text-field>
          </v-col>
        </v-row>
      </v-card-text>
      <v-card-actions>
        <v-btn color="primary">Guardar</v-btn>
        <v-btn color="error">Cancelar</v-btn>
      </v-card-actions>
    </v-card>
  </div>
</template>

<script>

export default {
  data() {
    return {
      idTarifa: '',
      tarifa: '',
      concepto: '',
      estatus: '',
      tipoProducto: '',
      tipoDocumento: '',
      diaInicio: '',
      diaFin: '',
      importe: '',
      aplicativos: []
    }
  },
}

</script>
