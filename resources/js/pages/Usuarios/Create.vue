<template>
  <AppLayout>
    <br><br>
    <div class="flex items-center justify-center max-w-4xl mx-auto bg-white dark:bg-gray-900 p-8 rounded-xl shadow-xl border border-blue-200">
      <!-- Formulario -->
      <div class="flex-1 max-w-md space-y-6">
        <!-- Encabezado con icono -->
        <div class="flex items-center gap-4 mb-6">
          <img
            src="https://cdn-icons-png.flaticon.com/512/3176/3176362.png"
            alt="Icono usuario"
            class="w-12 h-12"
          />
          <div>
            <h1 class="text-2xl font-bold text-blue-700">➕ Nuevo Usuario</h1>
            <p class="text-gray-500 text-sm">Completa el formulario para registrar un usuario</p>
          </div>
        </div>

        <!-- Formulario -->
        <form @submit.prevent="submitUsuario" class="space-y-5">
          <div>
            <label class="block text-sm font-medium text-gray-700 dark:text-white">👤 Nombre</label>
            <input v-model="form.nombre" type="text"
              class="mt-1 w-full rounded-md border border-gray-300 dark:border-gray-600 bg-white dark:bg-gray-900 text-gray-900 dark:text-white focus:ring-2 focus:ring-blue-500 focus:border-blue-500"
              required />
          </div>
          <div>
            <label class="block text-sm font-medium text-gray-700 dark:text-white">🧑 Usuario</label>
            <input v-model="form.usuario" type="text"
              class="mt-1 w-full rounded-md border border-gray-300 dark:border-gray-600 bg-white dark:bg-gray-900 text-gray-900 dark:text-white focus:ring-2 focus:ring-blue-500 focus:border-blue-500"
              required />
          </div>
          <div>
            <label class="block text-sm font-medium text-gray-700 dark:text-white">📧 Email</label>
            <input v-model="form.email" type="email"
              class="mt-1 w-full rounded-md border border-gray-300 dark:border-gray-600 bg-white dark:bg-gray-900 text-gray-900 dark:text-white focus:ring-2 focus:ring-blue-500 focus:border-blue-500"
              required />
          </div>
          <div>
            <label class="block text-sm font-medium text-gray-700 dark:text-white">🔒 Contraseña</label>
            <input v-model="form.contraseña" type="password"
              class="mt-1 w-full rounded-md border border-gray-300 dark:border-gray-600 bg-white dark:bg-gray-900 text-gray-900 dark:text-white focus:ring-2 focus:ring-blue-500 focus:border-blue-500"
              required />
          </div>
          <div class="flex justify-end gap-2">
            <Link :href="route('usuarios.index')" class="bg-gray-500 text-white px-4 py-2 rounded">Cancelar</Link>
            <button type="submit" class="bg-blue-500 text-white px-4 py-2 rounded">Guardar</button>
          </div>
        </form>
      </div>

      <!-- Imagen al lado del formulario -->
      <div class="hidden lg:block flex-shrink-0 ml-8">
        <img
          src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSni4W_ssx3U1KqS7a7wY_Q4NVU2hW3CP-1jA&s"
          alt="Imagen ilustrativa de usuario"
          class="w-80 h-100 object-cover rounded-lg shadow-xl"
        />
      </div>
      
    </div>
    <div class="min-h-[90vh] transition-colors duration-300
              bg-[#f7f9fc] text-gray-900
              dark:bg-gradient-to-br dark:from-black dark:to-[#0a2540] dark:text-white"></div>
  </AppLayout>
</template>

<script setup>
import { ref } from 'vue';
import { Link, router } from '@inertiajs/vue3';
import AppLayout from '@/layouts/AppLayout.vue';

const form = ref({
  nombre: '',
  usuario: '',
  email: '',
  contraseña: ''
});

const submitUsuario = () => {
  router.post(route('usuarios.store'), form.value);
};
</script>

<style scoped>
/* Estilo para los inputs con enfoque */
input:focus {
  border-color: #3b82f6;
  box-shadow: 0 0 0 1px rgba(59, 130, 246, 0.5);
}
</style>
