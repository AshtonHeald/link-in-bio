<script setup lang="ts">
import { Button } from '@/components/ui/button'
import type { Component } from 'vue'

interface SocialLink {
    href: string
    label: string
    icon: Component
}

interface Props {
    links: SocialLink[]
}

const props = defineProps<Props>()
</script>

<template>
    <div class="flex gap-x-4">
        <Button v-for="link in links" :key="link.href" variant="outline" size="icon" as-Child>
            <a :href="link.href" :aria-label="link.label">
                <component :is="link.icon" :size="24" />
            </a>
        </Button>
    </div>
</template>
