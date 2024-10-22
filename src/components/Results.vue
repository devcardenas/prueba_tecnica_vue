<template>
    <v-card :loading="loading">
        <v-table>
            <thead>
                <tr>
                    <th class="text-left">
                        #ID
                    </th>
                    <th class="text-left">
                        Tarifa
                    </th>
                    <th class="text-left">
                        Concepto
                    </th>
                    <th class="text-left">
                        Estatus
                    </th>
                    <th class="text-left">
                        Tipo de Producto
                    </th>
                    <th class="text-left">
                        Tipo de Documento
                    </th>
                    <th class="text-left">
                        Día Inicio
                    </th>
                    <th class="text-left">
                        Día Fin
                    </th>
                    <th class="text-left">
                        Importe
                    </th>
                    <th class="text-left">
                        Última Modificación
                    </th>
                    <th class="text-left">
                        Aplicativos
                    </th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="item in results" :key="item.idTarifa">
                    <td>{{ item.idTarifa }}</td>
                    <td>{{ item.tarifa }}</td>
                    <td>{{ item.concepto }}</td>
                    <td>{{ item.estatus.descripcion }}</td>
                    <td>{{ item.tipoProducto }}</td>
                    <td>{{ item.tipoDocumento.descripcion }}</td>
                    <td>{{ item.diaInicio }}</td>
                    <td>{{ item.diaFin }}</td>
                    <td>{{ item.importe }}</td>
                    <td>{{ item.fh_ultima_modificacion }}</td>
                    <td>
                        <ul v-for="ap in item.aplicativos" :key="ap.idAplicativo">
                            <li>{{ ap.aplicativo }} ({{ ap.cuotaAplicativo }})</li>
                        </ul>
                    </td>
                </tr>
            </tbody>
        </v-table>
    </v-card>
</template>
<script>
export default {
    props: {
        results: {
            type: Array,
            required: true,
        },
        loading: {
            type: Boolean,
            default: false,
        },
    },
}
</script>