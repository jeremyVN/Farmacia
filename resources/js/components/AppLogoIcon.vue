<script setup lang="ts">
import type { HTMLAttributes } from 'vue';

defineOptions({
    inheritAttrs: false,
});

interface Props {
    className?: HTMLAttributes['class'];
}

defineProps<Props>();
</script>

<template>
     <img
    :src="'https://thumbs.dreamstime.com/b/icono-de-farmacia-y-medicina-en-una-cruz-sobre-fondo-madera-azul-174947589.jpg'"
    alt="Icono de farmacia"
    :class="className"
    v-bind="$attrs"
  />
</template>
