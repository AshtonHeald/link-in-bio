<script setup lang="ts">
import { ref } from 'vue'
import { isClient } from '@vueuse/shared'
import { useShare, useClipboard } from '@vueuse/core'
import { Button } from '@/components/ui/button'
import { Tooltip, TooltipContent, TooltipProvider, TooltipTrigger } from '@/components/ui/tooltip'
import { PhShareFat, PhLinkSimple, PhLink } from '@phosphor-icons/vue'
// Set up the URL to be shared or copied
const url = ref(isClient ? location.href : '')

// Web Share API setup
const { share, isSupported: isShareSupported } = useShare({
    title: 'VueUse',
    text: 'Check out VueUse!',
    url: url.value
})

// Clipboard API setup
const { copy, copied, isSupported: isClipboardSupported } = useClipboard()

function startShare() {
    return share().catch((err) => err)
}

function copyUrl() {
    copy(url.value)
}
</script>

<template>
    <div>
        <!-- If Web Share API is supported, show the sharing button -->
        <div v-if="isShareSupported">
            <Button variant="ghost" size="icon" @click="startShare" class="h-7 w-7"><PhShareFat :size="16" /></Button>
        </div>

        <!-- If Web Share API is not supported, show the Clipboard button -->
        <div v-else-if="isClipboardSupported">
            <Button variant="ghost" size="icon" @click="copyUrl" class="h-7 w-7">
                <span v-if="!copied"><PhLinkSimple :size="16" /></span>
                <span v-else><PhLink :size="16" /></span>
            </Button>
        </div>

        <!-- Fallback if neither API is supported -->
        <p v-else></p>
    </div>
</template>
