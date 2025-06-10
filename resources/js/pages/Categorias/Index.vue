<template>
  <br>
  <div
    class="container mx-auto px-0 py-8 min-h-[90vh] transition-colors duration-300
           bg-[#f7f9fc] text-gray-900
           dark:bg-gradient-to-br dark:from-black dark:to-[#0a2540] dark:text-white"
  >

    <!-- Encabezado con imagen -->
    <div
      class="mx-auto bg-blue-50 dark:bg-gray-800 rounded-2xl p-6 mb-8 flex items-center justify-between"
      style="max-width: 97%; margin-right: auto; box-shadow: 0 10px 24px rgba(59, 130, 246, 0.4);"
    >
      <div>
        <h1 class="text-3xl font-bold text-blue-700 flex items-center gap-2">
          🗂️ Lista de Categorías
        </h1>
        <p class="text-gray-600 dark:text-gray-300 mt-1 text-sm">
          Administración y gestión de las categorías registradas en el sistema
        </p>
      </div>
      <img
        src="https://cdn-icons-png.flaticon.com/512/6381/6381854.png"
        alt="Categorías"
        class="w-16 h-16"
      />
    </div>

    <!-- Botón Crear -->
    <div class="max-w-6xl mx-4 flex justify-end mb-4">
      <Link
        :href="route('categorias.create')"
        class="bg-blue-600 hover:bg-blue-700 text-white font-medium px-5 py-2 rounded-full shadow-md transition-transform transform hover:scale-105"
      >
        ➕ Crear Categoría
      </Link>
    </div>

    <!-- Tabla de Categorías -->
    <div class="max-w-5xl mx-auto px-4">
      <div
        class="overflow-x-auto rounded-xl border border-blue-200 dark:border-gray-700 bg-white dark:bg-gray-800"
        style="box-shadow: 0 8px 24px rgba(59, 130, 246, 0.3);"
      >
        <table class="w-full min-w-max text-sm text-left text-gray-700 dark:text-gray-200">
          <thead class="bg-blue-600 text-white uppercase text-xs tracking-wider">
            <tr>
              <th class="px-4 py-3">📛 Nombre</th>
              <th class="px-4 py-3">📝 Descripción</th>
              <th class="px-4 py-3 text-center">⚙️</th>
            </tr>
          </thead>
          <transition-group name="fade" tag="tbody">
            <tr
              v-for="categoria in categorias.data"
              :key="categoria.id"
              class="border-b border-gray-200 dark:border-gray-700 hover:bg-blue-50 dark:hover:bg-gray-700 transition-colors"
            >
              <td class="px-4 py-3 text-gray-900 dark:text-white">{{ categoria.nombre }}</td>
              <td class="px-4 py-3 text-gray-900 dark:text-white">{{ categoria.descripcion }}</td>
              <td class="px-4 py-3 flex gap-3 justify-center items-center text-sm font-medium">
                <Link :href="route('categorias.show', categoria.id)" class="text-blue-600 hover:text-blue-400" title="Ver">
                  <Eye class="w-5 h-5" />
                </Link>
                <Link :href="route('categorias.edit', categoria.id)" class="text-indigo-500 hover:text-indigo-300" title="Editar">
                  <Pencil class="w-5 h-5" />
                </Link>
                <button @click="confirmDelete(categoria)" class="text-red-600 hover:text-red-400" title="Eliminar">
                  <Trash2 class="w-5 h-5" />
                </button>
              </td>
            </tr>
          </transition-group>
        </table>
      </div>
    </div>

    <!-- Paginación -->
    <div class="max-w-6xl mx-auto mt-6">
      <Pagination :links="categorias.links" />
    </div>
  </div>
</template>

<script setup>
import { Link, router } from '@inertiajs/vue3';
import Pagination from '@/components/Pagination.vue';
import AppSidebarLayout from '@/layouts/app/AppSidebarLayout.vue';
import { Trash2, Pencil, Eye } from 'lucide-vue-next';

defineProps({
  categorias: Object
});

const confirmDelete = (categoria) => {
  if (confirm('¿Estás seguro de que deseas eliminar esta categoría?')) {
    router.delete(route('categorias.destroy', categoria.id));
  }
};
</script>

<script>
export default {
  layout: AppSidebarLayout
};
</script>
