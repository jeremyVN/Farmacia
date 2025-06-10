<script setup lang="ts">
import { ref } from 'vue';
import NavMain from '@/components/NavMain.vue';
import NavUser from '@/components/NavUser.vue';
import {
  Sidebar,
  SidebarContent,
  SidebarFooter,
  SidebarHeader,
  SidebarMenu,
  SidebarMenuButton,
  SidebarMenuItem
} from '@/components/ui/sidebar';
import { type NavItem } from '@/types';
import { Link } from '@inertiajs/vue3';
import { BookOpen, Folder, LayoutGrid, ShoppingCart, Users, ChartColumnStacked, FileText, UserCheck, UserCog } from 'lucide-vue-next';
import AppLogo from './AppLogo.vue';

const isCollapsed = ref(false);

function toggleSidebar(state: boolean) {
  isCollapsed.value = state;
}

const mainNavItems: NavItem[] = [
  {
    title: 'Dashboard',
    href: '/dashboard',
    icon: LayoutGrid,
  },
  {
    title: 'Categorias',
    href: '/categorias',
    icon: ChartColumnStacked,
  },
  {
    title: 'Productos',
    href: '/productos',
    icon: ShoppingCart,
  },
  {
    title: 'Ventas',
    href: '/ventas',
    icon: ShoppingCart,
  },
  {
    title: 'Usuarios',
    href: '/usuarios',
    icon: Users,
  },

  {
        title: 'Reportes',
        href: '/reportes',
        icon: Users,
        children: [
            {
                title: 'Por Fecha',
                href: '/reporte/fecha',
                icon: FileText,
            },
            {
                title: 'Por Cliente',
                href: '/reporte/cliente',
                icon: UserCheck,
            },
            {
                title: 'Por Vendedor',
                href: '/reporte/vendedor',
                icon: UserCog,
            },
        ],
    },
];

const footerNavItems: NavItem[] = [
  {
    title: 'Github Repo',
    href: 'https://github.com/laravel/vue-starter-kit',
    icon: Folder,
  },
  {
    title: 'Documentation',
    href: 'https://laravel.com/docs/starter-kits',
    icon: BookOpen,
  },
];
</script>

<template>
  <Sidebar collapsible="icon" variant="inset">
    <!-- Logo Header -->
   <SidebarHeader class="pl-2"> <!-- Añado padding-left para ajustar manualmente -->
  <SidebarMenu class="flex justify-start"> <!-- Alinea todo a la izquierda -->
    <SidebarMenuItem>
      <SidebarMenuButton size="lg" as-child> <!-- Remueve padding interno -->
        <Link
          :href="route('dashboard')"
          class="flex items-center justify-start w-12 h-12 rounded-md overflow-hidden"
        >
          <AppLogo class="w-full h-full object-contain" />
        </Link>
      </SidebarMenuButton>
    </SidebarMenuItem>
  </SidebarMenu>
</SidebarHeader>


    <!-- Main Navigation -->
    <SidebarContent>
      <NavMain :items="mainNavItems" />
    </SidebarContent>

    <!-- Footer Links -->
    <SidebarFooter class="flex flex-col gap-4 p-4">
      <div class="flex flex-col gap-2 w-full">
        <a
  v-for="item in footerNavItems"
  :key="item.title"
  :href="item.href"
  :class="[
    'flex items-center gap-3 rounded-xl py-3 text-sm font-medium transition-colors',
    'text-blue-800 dark:text-blue-200',
    'bg-blue-100 dark:bg-blue-900 hover:bg-blue-200 dark:hover:bg-blue-700',
    isCollapsed ? 'justify-center px-0 w-12' : 'px-4 w-full'
  ]"
  target="_blank"
  rel="noopener noreferrer"
>
  <component :is="item.icon" class="w-5 h-5 shrink-0" />
  <span
    v-if="!isCollapsed"
    class="truncate whitespace-nowrap overflow-hidden flex-1"
  >
    {{ item.title }}
  </span>
</a>

      </div>
      <NavUser />
    </SidebarFooter>
  </Sidebar>

  <slot />
</template>
