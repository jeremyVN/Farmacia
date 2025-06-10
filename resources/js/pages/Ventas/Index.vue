<template>
  <AppSidebarLayout>
    <br />
    <div
      class="container mx-auto px-4 py-8 min-h-[90vh] transition-colors duration-300
             bg-[#f7f9fc] text-gray-900
             dark:bg-gradient-to-br dark:from-black dark:to-[#0a2540] dark:text-white"
    >
      <!-- Encabezado con imagen -->
      <div
        class="max-w-6xl mx-auto bg-blue-50 dark:bg-gray-800 rounded-2xl p-6 mb-8 flex items-center justify-between"
        style="box-shadow: 0 8px 24px rgba(59, 130, 246, 0.4);"
      >
        <div>
          <h1 class="text-3xl font-bold text-blue-700 flex items-center gap-2">
            🛒 Lista de Ventas
          </h1>
          <p class="text-gray-600 dark:text-gray-300 mt-1 text-sm">
            Gestión y control de las ventas realizadas
          </p>
        </div>
        <img
          src="https://cdn-icons-png.flaticon.com/512/1170/1170576.png"
          alt="Ventas"
          class="w-16 h-16"
        />
      </div>

      <!-- Botón de nueva venta -->
      <div class="max-w-6xl mx-auto flex justify-end mb-4">
        <Link
          :href="route('ventas.create')"
          class="bg-blue-600 hover:bg-blue-700 text-white font-medium px-5 py-2 rounded-full shadow-md transition-transform transform hover:scale-105"
        >
          ➕ Nueva Venta
        </Link>
      </div>

      <!-- Tabla de ventas -->
      <div class="max-w-6xl mx-auto">
        <div
          v-if="ventas.length"
          class="overflow-x-auto rounded-xl border border-blue-200 dark:border-gray-700 bg-white dark:bg-gray-800"
          style="box-shadow: 0 8px 24px rgba(59, 130, 246, 0.3);"
        >
          <table class="min-w-full text-sm text-left text-gray-700 dark:text-gray-200">
            <thead class="bg-blue-600 text-white uppercase text-xs tracking-wider">
              <tr>
                <th class="px-6 py-3">🆔 ID</th>
                <th class="px-6 py-3">👤 Cliente</th>
                <th class="px-6 py-3">🧑‍💼 Vendedor</th>
                <th class="px-6 py-3">💵 Total</th>
                <th class="px-6 py-3">📅 Fecha</th>
                <th class="px-6 py-3">⚙️ Acciones</th>
              </tr>
            </thead>
            <transition-group name="fade" tag="tbody">
              <tr
                v-for="venta in ventas"
                :key="venta.id"
                class="border-b border-gray-200 dark:border-gray-700 hover:bg-blue-50 dark:hover:bg-gray-700 transition-colors"
              >
                <td class="px-6 py-4 font-semibold text-blue-800 dark:text-blue-300">
                  {{ venta.id }}
                </td>
                <td class="px-6 py-4">{{ venta.cliente_nombre }}</td>
                <td class="px-6 py-4">{{ venta.usuario?.nombre }}</td>
                <td class="px-6 py-4">{{ venta.total }} Bs</td>
                <td class="px-6 py-4">{{ venta.fecha_registro }}</td>
                <td class="px-6 py-4 flex gap-4">
                  <Link
                    :href="route('ventas.show', venta.id)"
                    class="text-blue-600 hover:text-blue-400 font-medium"
                    title="Ver detalles"
                  >
                    👁️ Ver
                  </Link>
                  <button
                    @click="confirmDelete(venta)"
                    class="text-red-600 hover:text-red-400 font-medium"
                    title="Eliminar"
                  >
                    🗑️ Eliminar
                  </button>
                </td>
              </tr>
            </transition-group>
          </table>
        </div>

        <!-- Sin ventas -->
        <div v-else class="mt-16 text-center">
          <img
            src="https://cdn-icons-png.flaticon.com/512/4076/4076505.png"
            alt="Sin datos"
            class="mx-auto w-24 h-24 opacity-60"
          />
          <p class="mt-4 text-gray-500 dark:text-gray-400">No hay ventas registradas aún.</p>
        </div>
      </div>
    </div>
  </AppSidebarLayout>
</template>

<script setup>
import AppSidebarLayout from '@/layouts/app/AppSidebarLayout.vue';
import { Link } from '@inertiajs/vue3';
import { router } from '@inertiajs/vue3';

const props = defineProps({
  ventas: Array,
});

const confirmDelete = (venta) => {
  if (confirm(`¿Estás seguro de que deseas eliminar la venta #${venta.id}?`)) {
    router.delete(route('ventas.destroy', venta.id));
  }
};


</script>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: all 0.3s ease;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
  transform: translateY(10px);
}
</style>
