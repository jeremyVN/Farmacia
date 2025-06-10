<template>
  <AppSidebarLayout>
    <br>
    <div class=" min-h-[90vh] transition-colors duration-300
              bg-[#f7f9fc] text-gray-900
              dark:bg-gradient-to-br dark:from-black dark:to-[#0a2540] dark:text-white">
      <div class="container mx-auto px-4 py-8">
        
        <!-- Encabezado con imagen -->
        <div class="flex items-center justify-between bg-blue-50 dark:bg-slate-800 rounded-2xl shadow-lg shadow-blue-200 dark:shadow-blue-900 p-6 mb-6">
          <div>
            <h1 class="text-3xl font-extrabold text-blue-700 dark:text-blue-300 flex items-center gap-2">
              👥 Lista de Usuarios
            </h1>
            <p class="text-gray-600 dark:text-gray-300 mt-1">Gestión y control de los usuarios registrados</p>
          </div>
          <img
            src="https://cdn-icons-png.flaticon.com/512/747/747376.png"
            alt="Usuarios"
            class="w-16 h-16"
          />
        </div>

        <!-- Botón de nuevo usuario -->
        <div class="flex justify-end mb-4">
          <Link
            :href="route('usuarios.create')"
            class="bg-blue-600 hover:bg-blue-700 dark:bg-blue-700 dark:hover:bg-blue-800 text-white px-5 py-2 rounded-full shadow-lg shadow-blue-300 dark:shadow-blue-900 transition duration-300 ease-in-out transform hover:scale-105"
            as="button"
          >
            ➕ Nuevo Usuario
          </Link>
        </div>

        <!-- Tabla de usuarios -->
        <div v-if="usuarios.length">
          <div class="overflow-x-auto rounded-2xl shadow-lg shadow-blue-100 dark:shadow-blue-900 border border-blue-200 dark:border-blue-800 bg-white dark:bg-slate-900">
            <table class="min-w-full text-sm text-left text-gray-800 dark:text-gray-100">
              <thead class="bg-blue-600 dark:bg-blue-800 text-white uppercase text-xs tracking-wider">
                <tr>
                  <th class="px-6 py-3">📛 Nombre</th>
                  <th class="px-6 py-3">👤 Usuario</th>
                  <th class="px-6 py-3">📧 Email</th>
                  <th class="px-6 py-3">📅 Fecha Registro</th>
                  <th class="px-6 py-3">⚙️ Acciones</th>
                </tr>
              </thead>
              <transition-group name="fade" tag="tbody">
                <tr
                  v-for="usuario in usuarios"
                  :key="usuario.id"
                class="border-b border-blue-100 dark:border-blue-800 hover:bg-blue-100 dark:hover:bg-blue-900 transition-all duration-300 ease-in-out hover:shadow-md hover:shadow-blue-400/40 dark:hover:shadow-blue-800/60"
                >
                  <td class="px-6 py-4 font-semibold text-blue-800 dark:text-blue-200">{{ usuario.nombre }}</td>
                  <td class="px-6 py-4">{{ usuario.usuario }}</td>
                  <td class="px-6 py-4">{{ usuario.email }}</td>
                  <td class="px-6 py-4">{{ usuario.fecha_registro }}</td>
                  <td class="px-6 py-4 flex gap-3">
                    <Link
                      :href="route('usuarios.edit', usuario.id)"
                      class="text-indigo-600 dark:text-indigo-300 hover:text-indigo-400 font-medium"
                      title="Editar"
                    >
                      ✏️ Editar
                    </Link>
                    <button
                      @click="confirmDelete(usuario)"
                      class="text-red-600 dark:text-red-400 hover:text-red-400 font-medium"
                      title="Eliminar"
                    >
                      🗑️ Eliminar
                    </button>
                  </td>
                </tr>
              </transition-group>
            </table>
          </div>
        </div>

        <!-- Sin usuarios -->
        <div v-else class="mt-12 text-center">
          <img
            src="https://cdn-icons-png.flaticon.com/512/4076/4076505.png"
            alt="Sin datos"
            class="mx-auto w-24 h-24 opacity-60"
          />
          <p class="text-blue-500 dark:text-blue-300 mt-4 font-semibold text-lg animate-pulse">
            No hay usuarios registrados aún 🙁
          </p>
        </div>

      </div>
    </div>
  </AppSidebarLayout>
</template>

<script setup>
import { Link, router } from '@inertiajs/vue3';
import AppSidebarLayout from '@/layouts/app/AppSidebarLayout.vue';

defineProps({ usuarios: Array });

const confirmDelete = (usuario) => {
  if (confirm(`¿Estás seguro de que deseas eliminar a ${usuario.nombre}?`)) {
    router.delete(route('usuarios.destroy', usuario.id));
  }
};
</script>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: all 0.4s ease;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
  transform: translateY(10px);
}

/* Efecto brillo azul al pasar el cursor en las filas de la tabla */
tr.hover\:bg-blue-100:hover {
  background-color: #0930af; /* azul muy claro */
  box-shadow: 0 0 10px 2px #3b82f6; /* sombra azul (tailwind blue-500) */
  transition: background-color 0.3s ease, box-shadow 0.3s ease;
}
</style>
