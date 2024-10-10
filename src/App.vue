<script setup lang="ts">
import { Avatar, AvatarFallback, AvatarImage } from '@/components/ui/avatar'
import { Badge } from '@/components/ui/badge'
import { Tabs, TabsContent, TabsList, TabsTrigger } from '@/components/ui/tabs'
import { ScrollArea } from '@/components/ui/scroll-area'
import ThemeToggle from '@/components/ThemeToggle.vue'
import ShareButton from './components/ShareButton.vue'
import MainForm from '@/components/MenuForm.vue'
import SocialLinks from '@/components/SocialLinks.vue'
import MenuLinks from '@/components/MenuLinks.vue'

import ash from '@/assets/ash.png'
import {
    PhDevToLogo,
    PhGithubLogo,
    PhXLogo,
    PhHandHeart,
    PhHeadCircuit,
    PhCake,
    PhSealCheck,
    PhLinkedinLogo,
    PhHeartStraight,
    PhPlant,
    PhCode,
    PhSparkle
} from '@phosphor-icons/vue'
import { Toaster } from '@/components/ui/toast'

//--------------------------------------------------------------------------

const subHeading = 'Web Developer • Writer'

const socialLinks = [
    { href: 'https://x.com/ashtonheald', icon: PhXLogo },
    { href: 'https://www.linkedin.com/in/ashtonheald/', icon: PhLinkedinLogo },
    { href: 'https://dev.to/ashthedev', icon: PhDevToLogo },
    { href: 'https://github.com/ashtonheald', icon: PhGithubLogo },
    { href: 'https://buymeacoffee.com/ashtonheald', icon: PhHandHeart }
]
const menuLinks = [
    { href: 'https://ashthe.dev/', label: 'Web Portfolio', icon: PhCode, disabled: false },
    { href: 'https://cafe.ashtonheald.me/', label: 'Digital Garden', icon: PhPlant, disabled: false }
]
const showcaseLinks = [{ href: 'https://start.ashthe.dev/', label: 'Start Page', icon: PhSparkle }]
</script>

<template>
    <div
        className="h-screen w-full dark:bg-black bg-white  dark:bg-dot-white/[0.2] bg-dot-black/[0.2] relative grid place-items-center"
    >
        <div
            className="absolute pointer-events-none inset-0 flex items-center justify-center dark:bg-black bg-white [mask-image:radial-gradient(ellipse_at_center,transparent_20%,black)]"
        ></div>
        <div class="max-w-[300px]">
            <div class="flex w-full justify-between"></div>
            <div
                class="relative mt-[20px] rounded-lg border bg-card px-4 pb-2.5 pt-4 text-card-foreground shadow-sm sm:mt-0"
            >
                <header class="relative mb-4 grid place-items-center gap-4">
                    <div class="absolute top-[-48px]">
                        <Avatar size="lg">
                            <AvatarImage :src="ash" alt="Profile Image of Ashton" />
                            <AvatarFallback>AH</AvatarFallback>
                        </Avatar>
                    </div>
                    <div class="mb-[38px] flex w-full items-center justify-between gap-4">
                        <Badge variant="secondary" class="gap-1">
                            <PhCake :size="16" /> <span class="font-mono">1998</span>
                        </Badge>
                        <Badge variant="secondary" class="gap-1">
                            <PhHeadCircuit :size="16" /> <span class="font-mono">INTP</span>
                        </Badge>
                    </div>
                    <div class="text-center">
                        <h1 class="mb-0.5 flex items-center justify-center gap-1 text-xl font-bold">
                            Ashton G. Heald
                            <PhSealCheck :size="20" weight="fill" color="hotpink" class="mt-0.5" />
                        </h1>
                        <p class="text-sm">{{ subHeading }}</p>
                    </div>
                </header>
                <main class="mb-12 grid place-items-center space-y-4">
                    <SocialLinks :links="socialLinks" />
                    <Tabs default-value="links" class="w-full">
                        <TabsList class="mb-4 grid w-full grid-cols-2">
                            <TabsTrigger value="links"> Links </TabsTrigger>
                            <TabsTrigger value="contact"> Contact </TabsTrigger>
                        </TabsList>
                        <TabsContent value="links">
                            <MenuLinks :menuLinks="menuLinks" :showcaseLinks="showcaseLinks" />
                        </TabsContent>
                        <TabsContent value="contact">
                            <ScrollArea class="h-[184px]" type="always">
                                <MainForm />
                            </ScrollArea>
                        </TabsContent>
                    </Tabs>
                </main>
                <footer class="hidden items-center justify-between">
                    <ThemeToggle />
                    <div class="flex items-center justify-center gap-0.5 text-sm">
                        Made with <PhHeartStraight :size="14" class="mt-[1px]" />
                    </div>
                    <div class="flex gap-1">
                        <ShareButton />
                    </div>
                </footer>
            </div>
        </div>
        <Toaster />
    </div>
</template>
