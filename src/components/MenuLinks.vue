<script setup lang="ts">
import { Button } from '@/components/ui/button'
import { PhArrowUpRight, PhBarricade } from '@phosphor-icons/vue'
import type { Component } from 'vue'

interface MenuLink {
    href: string
    label: string
    icon: Component
}

interface ShowcaseLink {
    href: string
    label: string
    icon: Component
}

interface Props {
    menuLinks: MenuLink[]
    showcaseLinks: ShowcaseLink[]
}

const props = defineProps<Props>()
</script>

<template>
    <div class="mb-3 grid w-full max-w-xs gap-4">
        <Button v-for="link in menuLinks" :key="link.label" variant="outline" size="lg" as-Child>
            <a :href="link.href">
                <component :is="link.icon" :size="20" />
                {{ link.label }}
                <component :is="PhArrowUpRight" :size="16" class="ml-auto" weight="bold" />
            </a>
        </Button>
    </div>
    <div class="grid w-full max-w-xs space-y-1">
        <p class="text-sm font-semibold">Showcase</p>
        <Button v-for="link in showcaseLinks" :key="link.label" :href="link.href" variant="outline" size="lg" as-Child>
            <a :href="link.href">
                <component :is="link.icon" :size="20" />
                {{ link.label }}
                <component :is="PhArrowUpRight" :size="16" class="ml-auto" weight="bold" />
            </a>
        </Button>
    </div>
</template>
