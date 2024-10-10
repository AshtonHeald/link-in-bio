<script setup lang="ts">
import { AvatarImage, type AvatarImageProps } from 'radix-vue'

const props = defineProps<AvatarImageProps>()
</script>

<template>
    <AvatarImage v-bind="props" class="h-[110%] w-[110%] object-cover" />
</template>
