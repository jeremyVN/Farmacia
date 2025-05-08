<script setup lang="ts">
import NavFooter from '@/components/NavFooter.vue';
import NavMain from '@/components/NavMain.vue';
import NavUser from '@/components/NavUser.vue';
import { Sidebar, SidebarContent, SidebarFooter, SidebarHeader, SidebarMenu, SidebarMenuButton, SidebarMenuItem } from '@/components/ui/sidebar';
import { type NavItem } from '@/types';
import { Link } from '@inertiajs/vue3';
import { BookOpen, Folder, LayoutGrid } from 'lucide-vue-next';
import AppLogo from './AppLogo.vue';
import { ShoppingCart } from 'lucide-vue-next';
import { CalendarCog } from 'lucide-vue-next';
import { Users } from 'lucide-vue-next';
import { ChartColumnStacked } from 'lucide-vue-next';

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
        <SidebarHeader>
            
            <SidebarMenu>
                <SidebarMenuItem>
                    <SidebarMenuButton size="lg" as-child>
                        <Link :href="route('dashboard')">
                            <AppLogo />
                        </Link>
                    </SidebarMenuButton>
                </SidebarMenuItem>
            </SidebarMenu>
        </SidebarHeader>

        <SidebarContent>
            
            <NavMain :items="mainNavItems" />
        </SidebarContent>

        <SidebarFooter>
            <div class="flex gap-2">
    <a
      v-for="item in footerNavItems"
      :key="item.title"
      :href="item.href"
      class="flex items-center  rounded-lg bg-blue-800 px-3 py-2 text-sm text-blue-200 hover:bg-blue-300 transition-colors"
      target="_blank"
      rel="noopener noreferrer"
    >
      <component :is="item.icon" class="w-4 h-4" />
      {{ item.title }}
    </a>
  </div>
            <NavUser />
        </SidebarFooter>
       
    </Sidebar>
    
    <slot />
</template>
