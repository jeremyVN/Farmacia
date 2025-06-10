<template>
  <AppLayout>
    <div class="max-w-xl mx-auto bg-white dark:bg-gray-900 p-8 rounded-xl shadow-lg border border-blue-200">
      <!-- Encabezado -->
      <div class="flex items-center mb-6">
        <img
          src="https://cdn-icons-png.flaticon.com/512/3081/3081559.png"
          alt="Medicamento"
          class="w-12 h-12 mr-4"
        />
        <div>
          <h1 class="text-2xl font-bold text-blue-700 dark:text-blue-400">🏥 Reportes de Ventas - Farmacia</h1>
          <p class="text-gray-600 dark:text-gray-300 text-sm">Revisa el historial de ventas realizadas en tu farmacia</p>
        </div>
      </div>

      <!-- Tabla -->
      <div v-if="ventas.length" class="overflow-x-auto rounded-xl shadow-md border border-blue-200 bg-white dark:bg-gray-900 dark:border-blue-700">
        <table class="min-w-full text-sm text-left text-gray-700 dark:text-gray-300">
          <thead class="bg-blue-600 text-white uppercase text-xs tracking-wider dark:bg-blue-700">
            <tr>
              <th class="px-6 py-3">🧾 ID</th>
              <th class="px-6 py-3">👤 Cliente</th>
              <th class="px-6 py-3">💵 Total</th>
              <th class="px-6 py-3">📅 Fecha</th>
            </tr>
          </thead>
          <tbody>
            <tr
              v-for="venta in ventas"
              :key="venta.id"
              class="border-b border-gray-200 dark:border-blue-800 hover:bg-blue-50 dark:hover:bg-blue-900 transition"
            >
              <td class="px-6 py-4 font-semibold text-blue-800 dark:text-blue-400">{{ venta.id }}</td>
              <td class="px-6 py-4">{{ venta.cliente_nombre }}</td>
              <td class="px-6 py-4">{{ venta.total }}</td>
              <td class="px-6 py-4">{{ venta.fecha_registro }}</td>
            </tr>
          </tbody>
        </table>
      </div>

      <!-- Sin datos -->
      <div v-else class="mt-12 text-center">
        <img
          src="https://cdn-icons-png.flaticon.com/512/4149/4149623.png"
          alt="Sin datos"
          class="mx-auto w-24 h-24 opacity-60"
        />
        <p class="text-blue-500 mt-4 font-semibold text-lg animate-pulse dark:text-blue-400">
          No hay ventas disponibles por el momento 💤
        </p>
      </div>
    </div>
  </AppLayout>
</template>

<script setup>
import AppLayout from '@/layouts/AppLayout.vue';

const props = defineProps({
  ventas: {
    type: Array,
    required: true,
  },
});
</script>
