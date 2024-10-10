<script setup lang="ts">
import { useColorMode } from '@vueuse/core'
import { Button } from '@/components/ui/button'

const mode = useColorMode()
const isDark = ref(mode.value === 'dark')

// Function to toggle between light and dark modes
const toggleMode = () => {
    isDark.value = !isDark.value
    mode.value = isDark.value ? 'dark' : 'light'
}
import { ref } from 'vue'
import { PhMoonStars, PhSun } from '@phosphor-icons/vue'
</script>

<template>
    <Button variant="ghost" size="icon" @click="toggleMode" class="h-7 w-7">
        <Icon v-if="isDark" class="transition-all">
            <PhSun :size="16" />
        </Icon>
        <Icon v-else class="transition-all">
            <PhMoonStars :size="16" />
        </Icon>
        <span class="sr-only">Toggle theme</span>
    </Button>
</template>
