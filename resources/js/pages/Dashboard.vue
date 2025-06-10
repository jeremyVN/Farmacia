<script setup lang="ts">
import AppLayout from '@/layouts/AppLayout.vue';
import { type BreadcrumbItem } from '@/types';
import { Head } from '@inertiajs/vue3';
import { ref, onMounted } from 'vue';
import PlaceholderPattern from '../components/PlaceholderPattern.vue';
import BarChart from '@/components/BarChart.vue';


const breadcrumbs: BreadcrumbItem[] = [
  {
    title: 'Dashboard',
    href: '/dashboard',
  },
];

const hours = ref('00');
const minutes = ref('00');
const seconds = ref('00');
const period = ref('AM');
const is24Hour = ref(false);
const dateString = ref('');

const updateClock = () => {
  const now = new Date();
  let hrs = now.getHours();
  const mins = now.getMinutes();
  const secs = now.getSeconds();

  if (is24Hour.value) {
    hours.value = String(hrs).padStart(2, '0');
    period.value = '';
  } else {
    period.value = hrs >= 12 ? 'PM' : 'AM';
    hrs = hrs % 12 || 12;
    hours.value = String(hrs).padStart(2, '0');
  }

  minutes.value = String(mins).padStart(2, '0');
  seconds.value = String(secs).padStart(2, '0');

  const options: Intl.DateTimeFormatOptions = {
    weekday: 'long',
    month: 'short',
    day: 'numeric',
  };
  dateString.value = now.toLocaleDateString('en-US', options);
};

const toggleFormat = () => {
  is24Hour.value = !is24Hour.value;
};

onMounted(() => {
  updateClock();
  setInterval(updateClock, 1000);
});
defineProps(['productosVendidos', 'clientes', 'ventasPorMesLabels', 'ventasPorMesData'])
</script>

<template>
  <Head title="Dashboard" />

  <AppLayout :breadcrumbs="breadcrumbs">
    <div class="flex h-full flex-1 flex-col gap-4 rounded-xl p-4 ">
      <div class="grid auto-rows-min gap-4 md:grid-cols-3">
  <!-- Tarjeta 1: Productos Vendidos -->
 <!-- Tarjeta 1: Productos Vendidos (fondo azul suave) -->
<!-- Tarjeta 1: Productos Vendidos (degradado azul-naranja suave) -->
<div class="relative aspect-video overflow-hidden rounded-xl border border-sidebar-border/70 dark:border-sidebar-border bg-gradient-to-tr from-blue-100 to-orange-100 dark:from-blue-900 dark:to-orange-900 shadow p-4 flex flex-col justify-between">
  <PlaceholderPattern />
<div class="relative aspect-video overflow-hidden rounded-xl  bg-gradient-to-tr from-blue-100 to-orange-100 dark:from-blue-900 dark:to-orange-900 shadow p-4 flex flex-col items-center justify-center text-center">
  <PlaceholderPattern />
  <div class="text-6xl mb-2 z-10">🛒</div> <!-- Emoji centrado y grande -->
  <div>
    <h3 class="text-lg font-semibold text-gray-900 dark:text-white mb-1">PRODUCTOS VENDIDOS</h3>
    <p class="text-sm text-gray-800 dark:text-gray-300">Cantidad: {{ productosVendidos }}</p>
  </div>
</div>

</div>

<!-- Tarjeta 2: Clientes (degradado azul-naranja suave invertido) -->
<div class="relative aspect-video overflow-hidden rounded-xl border border-sidebar-border/70 dark:border-sidebar-border bg-gradient-to-tr from-orange-100 to-blue-100 dark:from-orange-900 dark:to-blue-900 shadow p-4 flex flex-col justify-between">
  <PlaceholderPattern />
  <div class="relative aspect-video overflow-hidden rounded-xl bg-gradient-to-tr from-orange-100 to-blue-100 dark:from-orange-900 dark:to-blue-900 shadow p-4 flex flex-col items-center justify-center text-center">
  <PlaceholderPattern />
  <div class="text-6xl mb-2 z-10">👥</div> <!-- Emoji centrado y grande -->
  <div>
    <h3 class="text-lg font-semibold text-gray-900 dark:text-white mb-1">CLIENTES</h3>
    <p class="text-sm text-gray-800 dark:text-gray-300">Cantidad: {{ clientes }}</p>
  </div>
</div>

</div>


  <!-- Tarjeta 3: Vacía o futura -->


  <!-- Celda 4: Reloj (NO se toca) -->
  <div class="relative aspect-video overflow-hidden rounded-xl border border-sidebar-border/70 dark:border-sidebar-border flex items-center justify-center bg-white dark:bg-[#1F1F2F] shadow-xl text-gray-900 dark:text-white">
    <!-- Botón de tres puntos -->
    <div class="absolute top-3 right-3 z-10">
      <button @click="toggleFormat" class="hover:text-gray-500 dark:hover:text-gray-300 text-xl">&#8942;</button>
    </div>

    <!-- Contenido del reloj -->
    <div class="flex flex-col items-center">
      <div class="text-6xl font-bold flex items-baseline justify-center gap-1">
        <span class="bg-gradient-to-r from-blue-500 to-orange-500 bg-clip-text text-transparent dark:from-blue-300 dark:to-orange-300">{{ hours }}</span>
        <span>:</span>
        <span class="bg-gradient-to-r from-orange-500 to-pink-500 bg-clip-text text-transparent dark:from-orange-300 dark:to-pink-300">{{ minutes }}</span>
        <span class="ml-3 text-base font-medium text-gray-600 dark:text-gray-400">{{ seconds }}s</span>
        <span v-if="!is24Hour" class="ml-2 text-yellow-500 dark:text-yellow-300 text-xl font-semibold">{{ period }}</span>
      </div>

      <!-- Fecha -->
      <div class="text-center mt-2 text-sm text-pink-500 dark:text-pink-300">
        {{ dateString }}
      </div>
    </div>
  </div>
</div>


      <!-- Área inferior -->
   <div class="relative min-h-[10vh] flex-1 rounded-xl border border-sidebar-border/70 dark:border-sidebar-border 
            md:min-h-min bg-[#f7f9fc] text-gray-900 dark:bg-gradient-to-br dark:from-black dark:to-[#0a2540] 
            dark:text-white transition-colors duration-300 p-4">
  
  <div class="grid md:grid-cols-2 gap-4">
    <!-- Gráfico 1 -->
   <div class="flex flex-col rounded-xl p-4 shadow-lg border border-gray-300 
            bg-gradient-to-br from-blue-50 to-blue-100 
            dark:from-gray-800 dark:to-gray-900 transition duration-300 
            min-h-[300px]">
  <h3 class="mb-2 text-lg font-bold flex items-center gap-2">
    📊 Ventas por Mes
  </h3>
  <hr class="my-2 border-blue-300 dark:border-gray-700">
  <div class="flex-1">
    <transition name="fade" mode="out-in">
      <BarChart
        :labels="ventasPorMesLabels"
        :values="ventasPorMesData"
        label="Ventas"
      />
    </transition>
  </div>
</div>


    <!-- Gráfico 2 -->
     
   <div class="flex flex-col rounded-xl p-4 shadow-lg border border-gray-300 
            bg-gradient-to-br from-blue-50 to-blue-100 
            dark:from-gray-800 dark:to-gray-900 transition duration-300 
            min-h-[300px]">
  <h3 class="mb-2 text-lg font-bold flex items-center gap-2">
    📊 Ventas por Mes
  </h3>
  <hr class="my-2 border-blue-300 dark:border-gray-700">
  <div class="flex-1">
    <transition name="fade" mode="out-in">
      <BarChart
        :labels="ventasPorMesLabels"
        :values="ventasPorMesData"
        label="Ventas"
      />
    </transition>
  </div>
</div>

  </div>
</div>


    </div>
  </AppLayout>
</template>
