<script setup lang="ts">
import { useForm } from 'vee-validate'
import { toTypedSchema } from '@vee-validate/zod'
import * as z from 'zod'
import { vAutoAnimate } from '@formkit/auto-animate/vue'
import emailjs from '@emailjs/browser'
import { Button } from '@/components/ui/button'
import { FormControl, FormField, FormItem, FormLabel, FormMessage } from '@/components/ui/form'
import { Textarea } from '@/components/ui/textarea'
import { Input } from '@/components/ui/input'
import { useToast } from '@/components/ui/toast/use-toast'

const formSchema = toTypedSchema(
    z.object({
        name: z
            .string()
            .min(2, 'Name must be at least 2 characters')
            .max(50, 'Name must not exceed 50 characters')
            .regex(/^[a-zA-Z\s'-]+$/, 'Name can only contain letters, spaces, hyphens, and apostrophes'),

        email: z.string().email('Please enter a valid email address').max(100, 'Email must not exceed 100 characters'),

        subject: z
            .string()
            .min(2, 'Subject must be at least 2 characters')
            .max(100, 'Subject must not exceed 100 characters'),

        message: z
            .string()
            .min(10, 'Message must be at least 10 characters')
            .max(1000, 'Message must not exceed 1000 characters')
    })
)

const form = useForm({
    validationSchema: formSchema
})

const { toast } = useToast()

import { ref } from 'vue'

const formRef = ref<HTMLFormElement | null>(null)

const onSubmit = form.handleSubmit((values, { resetForm }) => {
    if (formRef.value) {
        emailjs
            .sendForm('contact_service', 'links_form', formRef.value, {
                publicKey: '8PhuMhkMRUrBunrkl'
            })
            .then(
                () => {
                    toast({
                        description: 'Your message has been sent.'
                    })
                    resetForm()
                },
                (error) => {
                    toast({
                        variant: 'destructive',
                        title: 'Uh oh! Something went wrong.',
                        description: error.text || 'There was an error submitting the form.'
                    })
                    console.log('FAILED...', error.text)
                }
            )
    } else {
        toast({
            variant: 'destructive',
            title: 'Uh oh! Something went wrong.',
            description: '404 Form not found.'
        })
        console.error('Form not found.')
    }
})
</script>

<template>
    <p class="mb-3 text-sm font-semibold">Send me a message</p>
    <form @submit="onSubmit" ref="formRef" class="space-y-4 pr-4">
        <FormField v-slot="{ componentField }" name="name">
            <FormItem class="relative" v-auto-animate>
                <FormControl>
                    <Input type="text" placeholder="Name" v-bind="componentField" />
                </FormControl>
                <FormLabel class="absolute font-normal text-muted-foreground">Name</FormLabel>
                <FormMessage />
            </FormItem>
        </FormField>
        <FormField v-slot="{ componentField }" name="email">
            <FormItem class="relative" v-auto-animate>
                <FormControl>
                    <Input type="email" placeholder="Email" v-bind="componentField" />
                </FormControl>
                <FormLabel class="absolute font-normal text-muted-foreground">Email</FormLabel>
                <FormMessage />
            </FormItem>
        </FormField>
        <FormField v-slot="{ componentField }" name="subject">
            <FormItem class="relative" v-auto-animate>
                <FormControl>
                    <Input type="text" placeholder="Subject" v-bind="componentField" />
                </FormControl>
                <FormLabel class="absolute font-normal text-muted-foreground">Subject</FormLabel>
                <FormMessage />
            </FormItem>
        </FormField>
        <FormField v-slot="{ componentField }" name="message">
            <FormItem class="relative" v-auto-animate>
                <FormControl>
                    <Textarea id="message" placeholder="Message" v-bind="componentField" />
                </FormControl>
                <FormLabel class="absolute font-normal text-muted-foreground">Message</FormLabel>
                <FormMessage />
            </FormItem>
        </FormField>
        <Button variant="outline" size="sm" type="submit"> Submit </Button>
    </form>
</template>

<style>
form label {
    left: 14px;
    top: 3px;
    pointer-events: none;
}
form input:focus ~ label,
form textarea:focus ~ label,
form input:not(:placeholder-shown) ~ label,
form textarea:not(:placeholder-shown) ~ label {
    background: hsl(var(--background));
    top: -16px;
    left: 6px;
    display: block;
    line-height: 1;
    font-size: 12px;
    padding: 0 2px !important;
    color: hsl(var(--foreground));
    transition-duration: 100ms;
}

input[type='text']:-moz-placeholder,
input[type='email']:-moz-placeholder,
textarea[id='message']:-moz-placeholder {
    color: hsl(var(--foreground));
    opacity: 0;
}
input[type='text']::-moz-placeholder,
input[type='email']::-moz-placeholder,
textarea[id='message']::-moz-placeholder {
    color: hsl(var(--foreground));
    opacity: 0;
}
input[type='text']:-ms-input-placeholder,
input[type='email']:-ms-input-placeholder,
textarea[id='message']:-ms-input-placeholder {
    color: hsl(var(--foreground));
    opacity: 0;
}
input[type='text']::-webkit-input-placeholder,
input[type='email']::-webkit-input-placeholder,
textarea[id='message']::-webkit-input-placeholder {
    color: transparent;
}
</style>
