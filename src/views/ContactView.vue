<script setup>
import { ref } from 'vue'
import emailjs from '@emailjs/browser';
import {
  IconMail,
  IconMapPin,
  IconBrandLinkedin,
  IconBrandGithub,
  IconBrandInstagram,
  IconSend,
  IconLoader2,
  IconCheck
} from '@tabler/icons-vue'

const isSubmitting = ref(false)
const isSuccess = ref(false)
const isError = ref(false)
const formData = ref({
  name: '',
  email: '',
  message: ''
})

const errors = ref({
  name: '',
  email: '',
  message: ''
})

const handleSubmit = async () => {
  errors.value = { name: '', email: '', message: '' }
  let isValid = true

  if (!formData.value.name) {
    errors.value.name = 'error_name_required'
    isValid = false
  }

  if (!formData.value.email) {
    errors.value.email = 'error_email_required'
    isValid = false
  } else if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(formData.value.email)) {
    errors.value.email = 'error_email_invalid'
    isValid = false
  }

  if (!formData.value.message) {
    errors.value.message = 'error_message_required'
    isValid = false
  }

  if (!isValid) return;

  isSubmitting.value = true
  isError.value = false

  try {
    const response = await emailjs.send(
      import.meta.env.VITE_EMAILJS_SERVICE_ID,
      import.meta.env.VITE_EMAILJS_TEMPLATE_ID,
      {
        name: formData.value.name,
        email: formData.value.email,
        message: formData.value.message,
      },
      import.meta.env.VITE_EMAILJS_PUBLIC_KEY
    )

    if (response.status === 200) {
      isSuccess.value = true
      formData.value = { name: '', email: '', message: '' }

      setTimeout(() => {
        isSuccess.value = false
      }, 5000)
    }
  } catch (error) {
    console.error('Error submitting form:', error)
    isError.value = true
    setTimeout(() => {
      isError.value = false
    }, 5000)
  } finally {
    isSubmitting.value = false
  }
}

const socialLinks = [
  {
    name: 'GitHub',
    icon: IconBrandGithub,
    href: 'https://github.com/apriandhitaaries'
  },
  {
    name: 'LinkedIn',
    icon: IconBrandLinkedin,
    href: 'https://www.linkedin.com/in/apriandhitaap/'
  },
  {
    name: 'Instagram',
    icon: IconBrandInstagram,
    href: 'https://instagram.com/apriandhita.aries'
  }
]
</script>

<template>
  <main class="max-w-7xl mx-auto px-6 md:px-12 pt-8 md:pt-12 pb-24 min-h-screen relative">
    <transition
      enter-active-class="transition duration-300 ease-out"
      enter-from-class="opacity-0 -translate-y-4 sm:-translate-y-8"
      enter-to-class="opacity-100 translate-y-0"
      leave-active-class="transition duration-200 ease-in"
      leave-from-class="opacity-100 translate-y-0"
      leave-to-class="opacity-0 -translate-y-4 sm:-translate-y-8"
    >
      <div
        v-if="isSuccess"
        class="fixed top-4 left-1/2 -translate-x-1/2 z-50 flex items-center gap-3 px-6 py-4 bg-emerald-100/90 backdrop-blur-sm border border-emerald-200 text-emerald-600 rounded-xl shadow-lg"
      >
        <IconCheck class="w-5 h-5" />
        <span class="text-sm font-medium">{{ $t('message_success') }}</span>
      </div>
    </transition>

    <div class="grid grid-cols-1 lg:grid-cols-12 gap-12 lg:gap-16 items-start mt-8">
      <!-- Left Column: Info & Socials -->
      <div class="lg:col-span-5 flex flex-col justify-center">

        <h1 class="text-4xl md:text-5xl font-extrabold text-zinc-900 tracking-tight mb-4">
          {{ $t('Get in Touch') }}
        </h1>

        <p class="text-zinc-500 text-base md:text-lg leading-relaxed mb-10 max-w-md">
          {{ $t('contact_desc') }}
        </p>

        <!-- Contact items -->
        <div class="space-y-6 mb-12">
          <!-- Email -->
          <div class="flex items-center gap-4">
            <div
              class="w-12 h-12 rounded-xl bg-zinc-50 border-2 border-zinc-200 flex items-center justify-center text-zinc-800 shrink-0"
            >
              <IconMail class="w-6 h-6" />
            </div>
            <div>
              <p class="text-[11px] font-bold text-zinc-400 tracking-wider uppercase mb-0.5">
                {{ $t('EMAIL') }}
              </p>
              <p class="text-zinc-900 font-semibold">
                apriandhita.work@gmail.com
              </p>
            </div>
          </div>

          <!-- Location -->
          <div class="flex items-center gap-4">
            <div
              class="w-12 h-12 rounded-xl bg-zinc-50 border-2 border-zinc-200 flex items-center justify-center text-zinc-800 shrink-0"
            >
              <IconMapPin class="w-6 h-6" />
            </div>
            <div>
              <p class="text-[11px] font-bold text-zinc-400 tracking-wider uppercase mb-0.5">
                {{ $t('LOCATION') }}
              </p>
              <p class="text-zinc-900 font-semibold">
                Indonesia
              </p>
            </div>
          </div>
        </div>

        <!-- Social Links -->
        <div>
          <p class="text-[11px] font-bold text-zinc-400 tracking-wider uppercase mb-4">
            {{ $t('FIND ME ON') }}
          </p>
          <div class="flex items-center gap-3">
            <a
              v-for="social in socialLinks"
              :key="social.name"
              :href="social.href"
              target="_blank"
              rel="noopener noreferrer"
              :title="social.name"
              class="w-11 h-11 rounded-xl bg-white border-2 border-zinc-200 flex items-center justify-center text-zinc-600 hover:text-zinc-900 hover:border-zinc-900 hover:bg-zinc-50 hover:-translate-y-0.5 transition-all duration-200 shadow-sm"
            >
              <component :is="social.icon" class="w-5 h-5" />
            </a>
          </div>
        </div>
      </div>

      <!-- Right Column: Form Card -->
      <div class="lg:col-span-7">
        <div class="bg-white border-2 border-zinc-200 rounded-2xl md:rounded-3xl p-6 sm:p-8 md:p-10 shadow-sm hover:border-zinc-300 transition-colors">
          <h2 class="text-xl md:text-2xl font-bold text-zinc-900 mb-8">
            {{ $t('Send a Message') }}
          </h2>

          <form @submit.prevent="handleSubmit" class="space-y-6" novalidate>
            <div class="grid grid-cols-1 sm:grid-cols-2 gap-5">

              <!-- Name Input -->
              <div>
                <label for="name" class="block text-[11px] font-bold tracking-wider uppercase mb-2 transition-colors" :class="errors.name ? 'text-red-500' : 'text-zinc-600'">
                  {{ $t('YOUR NAME') }}
                </label>
                <input
                  id="name"
                  v-model="formData.name"
                  @input="errors.name = ''"
                  type="text"
                  placeholder="John Doe"
                  :class="errors.name ? 'border-red-500 focus:border-red-500 focus:ring-red-500' : 'border-zinc-200 focus:border-zinc-900 focus:ring-zinc-900'"
                  class="w-full bg-zinc-50 border rounded-xl px-4 py-3.5 text-zinc-900 placeholder-zinc-400 focus:outline-none focus:ring-2 transition-all"
                  :disabled="isSubmitting"
                />
                <p v-if="errors.name" class="text-red-500 text-xs font-medium mt-1.5">{{ $t(errors.name) }}</p>
              </div>

              <!-- Email Input -->
              <div>
                <label for="email" class="block text-[11px] font-bold tracking-wider uppercase mb-2 transition-colors" :class="errors.email ? 'text-red-500' : 'text-zinc-600'">
                  {{ $t('EMAIL ADDRESS') }}
                </label>
                <input
                  id="email"
                  v-model="formData.email"
                  @input="errors.email = ''"
                  type="email"
                  placeholder="john@example.com"
                  :class="errors.email ? 'border-red-500 focus:border-red-500 focus:ring-red-500' : 'border-zinc-200 focus:border-zinc-900 focus:ring-zinc-900'"
                  class="w-full bg-zinc-50 border rounded-xl px-4 py-3.5 text-zinc-900 placeholder-zinc-400 focus:outline-none focus:ring-2 transition-all"
                  :disabled="isSubmitting"
                />
                <p v-if="errors.email" class="text-red-500 text-xs font-medium mt-1.5">{{ $t(errors.email) }}</p>
              </div>
            </div>

            <!-- Message Textarea -->
            <div>
              <label for="message" class="block text-[11px] font-bold tracking-wider uppercase mb-2 transition-colors" :class="errors.message ? 'text-red-500' : 'text-zinc-600'">
                {{ $t('MESSAGE') }}
              </label>
              <textarea
                id="message"
                v-model="formData.message"
                @input="errors.message = ''"
                rows="6"
                :placeholder="$t('tell_me_placeholder')"
                :class="errors.message ? 'border-red-500 focus:border-red-500 focus:ring-red-500' : 'border-zinc-200 focus:border-zinc-900 focus:ring-zinc-900'"
                class="w-full bg-zinc-50 border rounded-xl p-4 text-zinc-900 placeholder-zinc-400 focus:outline-none focus:ring-2 transition-all resize-none"
                :disabled="isSubmitting"
              ></textarea>
              <p v-if="errors.message" class="text-red-500 text-xs font-medium mt-1.5">{{ $t(errors.message) }}</p>
            </div>

            <!-- Submit Button (Loading State) -->
            <button
              type="submit"
              :disabled="isSubmitting"
              class="w-full py-4 px-6 rounded-xl bg-zinc-900 text-white font-bold flex items-center justify-center gap-2.5 transition-all duration-300 shadow-md"
              :class="isSubmitting ? 'opacity-80 cursor-wait' : 'hover:bg-zinc-800 hover:-translate-y-0.5 shadow-zinc-900/10 cursor-pointer active:translate-y-0'"
            >
              <!-- Menampilkan icon loading berputar saat submit -->
              <IconLoader2 v-if="isSubmitting" class="w-5 h-5 animate-spin" />
              <!-- Teks tombol berubah saat loading, atau kembali semula -->
              <template v-else>
                <IconSend class="w-5 h-5" />
                <span>{{ $t('Send Message') }}</span>
              </template>
              <span v-if="isSubmitting">{{ $t('Sending...') }}</span>
            </button>
          </form>
        </div>
      </div>
    </div>
  </main>
</template>
