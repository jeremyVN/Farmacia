<script setup lang="ts">
import Breadcrumbs from '@/components/Breadcrumbs.vue';
import { SidebarTrigger } from '@/components/ui/sidebar';
import type { BreadcrumbItemType } from '@/types';
import { ref, watchEffect } from 'vue';

// Importar íconos desde lucide-vue-next
import { Settings, Bell, Sun, Moon } from 'lucide-vue-next';

// Control del tema
const isDark = ref(false);

function toggleTheme() {
  isDark.value = !isDark.value;
  document.documentElement.classList.toggle('dark', isDark.value);
}

watchEffect(() => {
  localStorage.setItem('theme', isDark.value ? 'dark' : 'light');
});

withDefaults(defineProps<{
  breadcrumbs?: BreadcrumbItemType[];
}>(), {
  breadcrumbs: () => []
});
</script>

<template>
  <header
    class="flex h-16 shrink-0 items-center justify-center gap-4 px-6 transition-[width,height] ease-linear group-has-data-[collapsible=icon]/sidebar-wrapper:h-12 md:px-4 
           rounded-3xl shadow-lg shadow-blue-500/50 bg-white dark:bg-gray-800 border border-gray-300 dark:border-gray-700"
  >
    <div class="flex items-center gap-4">
      <SidebarTrigger class="-ml-1" />

      <button class="text-gray-600 dark:text-gray-300 hover:text-blue-600 dark:hover:text-white transition">
        <Settings class="w-5 h-5" />
      </button>

      <button class="text-gray-600 dark:text-gray-300 hover:text-blue-600 dark:hover:text-white transition">
        <Bell class="w-5 h-5" />
      </button>

      <button
        class="text-gray-600 dark:text-gray-300 hover:text-blue-600 dark:hover:text-white transition"
        @click="toggleTheme"
        title="Cambiar tema"
      >
        <Sun v-if="!isDark" class="w-5 h-5" />
        <Moon v-else class="w-5 h-5" />
      </button>
    </div>
  </header>
</template>

