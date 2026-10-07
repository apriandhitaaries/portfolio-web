<script setup>
import { ref, onMounted, computed } from 'vue'

const roles = ['Android Developer.', 'Full-stack Web Developer.', 'Tech Enthusiast.']

const displayText = ref('')
const isDeleting = ref(false)
let loopNum = ref(0)
let typingSpeed = 100

// Compute the correct article ("A" or "An") based on the current role
const article = computed(() => {
  const currentRole = roles[loopNum.value % roles.length]
  const firstLetter = currentRole.charAt(0).toLowerCase()
  return ['a', 'e', 'i', 'o', 'u'].includes(firstLetter) ? 'An' : 'A'
})

// Type effect function
const typeEffect = () => {
  const currentRole = roles[loopNum.value % roles.length]

  if (isDeleting.value) {
    displayText.value = currentRole.substring(0, displayText.value.length - 1)
    typingSpeed = 50
  } else {
    displayText.value = currentRole.substring(0, displayText.value.length + 1)
    typingSpeed = 100
  }

  if (!isDeleting.value && displayText.value === currentRole) {
    typingSpeed = 2000
    isDeleting.value = true
  } else if (isDeleting.value && displayText.value === '') {
    isDeleting.value = false
    loopNum.value++
    typingSpeed = 500
  }

  setTimeout(typeEffect, typingSpeed)
}

onMounted(() => {
  typeEffect()
})
</script>

<template>
  <main class="flex flex-col items-center justify-center text-center px-6 mt-32 min-h-[50vh]">
    <h1 class="text-5xl md:text-7xl font-extrabold mb-4 tracking-tight">
      {{ $t('hero_greeting') }}
    </h1>

    <div class="h-10 mb-6">
      <p class="text-2xl md:text-3xl text-gray-500 font-medium">
        {{ article }} <span class="text-black">{{ displayText }}</span
        ><span class="animate-pulse text-black">|</span>
      </p>
    </div>

    <p class="text-lg text-gray-600 max-w-2xl mb-10 leading-relaxed">
      {{ $t('hero_desc') }}
    </p>

    <div class="flex flex-col sm:flex-row gap-4 w-full sm:w-auto px-4 sm:px-0 mt-4">
      <RouterLink
        to="/projects"
        class="inline-block text-center px-8 py-3.5 rounded-full bg-zinc-900 text-white font-bold hover:bg-zinc-800 transition-all shadow-lg shadow-zinc-900/20 hover:-translate-y-0.5"
      >
        {{ $t('View Projects') }}
      </RouterLink>

      <RouterLink
        to="/contact"
        class="inline-block text-center px-8 py-3.5 rounded-full border-2 border-zinc-200 text-zinc-900 font-bold hover:border-zinc-900 hover:bg-zinc-50 transition-all"
      >
        {{ $t('Get in Touch') }}
      </RouterLink>
    </div>
  </main>
</template>
