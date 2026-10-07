<script setup>
import { ref, computed } from 'vue'
import {
  IconDeviceMobile,
  IconBrowser,
  IconDatabase,
  IconBriefcase,
  IconSchool,
  IconCertificate,
  IconChevronLeft,
  IconChevronRight,
  IconFileDescription,
} from '@tabler/icons-vue'

const certificates = [
  {
    title: 'Memulai Pemrograman dengan Dart',
    date: 'Nov 2025',
    link: 'https://www.dicoding.com/certificates/NVP7JN3YVXR0',
  },
  {
    title: 'Belajar Pengembangan Aplikasi Android Intermediate',
    date: 'May 2024',
    link: 'https://www.dicoding.com/certificates/RVZKRRDGOPD5',
  },
  {
    title: 'Belajar Dasar AI',
    date: 'Apr 2024',
    link: 'https://www.dicoding.com/certificates/GRX5OG7DYP0M',
  },
  {
    title: 'Belajar Penerapan Machine Learning untuk Android',
    date: 'Apr 2024',
    link: 'https://www.dicoding.com/certificates/72ZDVO9M6ZYW',
  },
  {
    title: 'Belajar Prinsip Pemrograman SOLID',
    date: 'Apr 2024',
    link: 'https://www.dicoding.com/certificates/MRZME5L8NPYQ',
  },
  {
    title: 'Belajar Fundamental Aplikasi Android',
    date: 'Mar 2024',
    link: 'https://www.dicoding.com/certificates/JMZVDY0KRZN9',
  },
  {
    title: 'Belajar Membuat Aplikasi Android untuk Pemula',
    date: 'Mar 2024',
    link: 'https://www.dicoding.com/certificates/6RPNV2WL4Z2M',
  },
  {
    title: 'Memulai Pemrograman dengan Kotlin',
    date: 'Feb 2024',
    link: 'https://www.dicoding.com/certificates/QLZ94E387P5D',
  },
  {
    title: 'Memulai Pemrograman dengan Java',
    date: 'Feb 2024',
    link: 'https://www.dicoding.com/certificates/JMZVD0MJRZN9',
  },
  {
    title: 'Belajar Dasar Git dengan GitHub',
    date: 'Feb 2024',
    link: 'https://www.dicoding.com/certificates/81P2V611YPOY',
  },
  {
    title: 'Memulai Dasar Pemrograman untuk Menjadi Pengembang Software',
    date: 'Feb 2024',
    link: 'https://www.dicoding.com/certificates/EYX40Q06WPDL',
  },
  {
    title: 'Pengenalan ke Logika Pemrograman (Programming Logic 101)',
    date: 'Feb 2024',
    link: 'https://www.dicoding.com/certificates/N9ZOON5J0ZG5',
  },
]

const currentPage = ref(0)
const itemsPerPage = 6

const totalPages = computed(() => Math.ceil(certificates.length / itemsPerPage))

const paginatedCertificates = computed(() => {
  const start = currentPage.value * itemsPerPage
  return certificates.slice(start, start + itemsPerPage)
})

const nextPage = () => {
  if (currentPage.value < totalPages.value - 1) {
    currentPage.value++
  }
}

const prevPage = () => {
  if (currentPage.value > 0) {
    currentPage.value--
  }
}
</script>

<template>
  <main class="max-w-7xl mx-auto px-6 md:px-12 pt-10 pb-24 min-h-screen">
    <section class="mb-16">
      <h1 class="text-5xl md:text-7xl font-extrabold text-zinc-900 tracking-tighter mb-6">
        {{ $t('About Me.') }}
      </h1>
      <p class="text-xl md:text-2xl text-zinc-500 max-w-3xl leading-relaxed">
        {{ $t('about_me_desc') }}
      </p>
    </section>

    <section class="flex flex-col md:flex-row gap-12 md:gap-20 mb-24">
      <div class="w-full md:w-1/3">
        <div
          class="aspect-[4/5] bg-zinc-100 border-2 border-zinc-200 rounded-2xl flex items-center justify-center overflow-hidden"
        >
          <img
            src="../assets/profile.webp"
            alt="Apriandhita Aries"
            class="w-full h-full object-cover filter grayscale hover:grayscale-0 transition duration-500"
          />
        </div>
      </div>

      <div class="w-full md:w-2/3 flex flex-col justify-center">
        <h2 class="text-2xl font-bold text-zinc-900 mb-4 border-b-2 border-zinc-900 pb-2 w-max">
          {{ $t('The Journey') }}
        </h2>
        <div class="text-lg text-zinc-600 space-y-6 leading-relaxed">
          <p>
            {{ $t('journey_paragraph_1') }}
          </p>
          <p>
            {{ $t('journey_paragraph_2') }}
          </p>
          <p>
            {{ $t('journey_paragraph_3') }}
          </p>
        </div>
      </div>
    </section>

    <section class="mb-24">
      <h2 class="text-2xl font-bold text-zinc-900 mb-8 border-b-2 border-zinc-900 pb-2 w-max">
        {{ $t('Core Focus') }}
      </h2>

      <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
        <div
          class="p-8 border-2 border-zinc-200 rounded-2xl hover:border-zinc-900 transition-colors group bg-white"
        >
          <IconBrowser
            class="w-10 h-10 text-zinc-900 mb-6 group-hover:-translate-y-1 transition-transform"
            stroke-width="1.5"
          />
          <h3 class="text-xl font-bold text-zinc-900 mb-3">{{ $t('Frontend Dev') }}</h3>
          <p class="text-zinc-500">
            {{ $t('frontend_desc') }}
          </p>
        </div>

        <div
          class="p-8 border-2 border-zinc-200 rounded-2xl hover:border-zinc-900 transition-colors group bg-white"
        >
          <IconDeviceMobile
            class="w-10 h-10 text-zinc-900 mb-6 group-hover:-translate-y-1 transition-transform"
            stroke-width="1.5"
          />
          <h3 class="text-xl font-bold text-zinc-900 mb-3">{{ $t('Android Native') }}</h3>
          <p class="text-zinc-500">
            {{ $t('android_desc') }}
          </p>
        </div>

        <div
          class="p-8 border-2 border-zinc-200 rounded-2xl hover:border-zinc-900 transition-colors group bg-white"
        >
          <IconDatabase
            class="w-10 h-10 text-zinc-900 mb-6 group-hover:-translate-y-1 transition-transform"
            stroke-width="1.5"
          />
          <h3 class="text-xl font-bold text-zinc-900 mb-3">{{ $t('Backend & Systems') }}</h3>
          <p class="text-zinc-500">
            {{ $t('backend_desc') }}
          </p>
        </div>
      </div>
    </section>

    <!-- 1. EXPERIENCE SECTION -->
    <section class="mb-16">
      <h2 class="text-2xl font-bold text-zinc-900 mb-8 border-b-2 border-zinc-900 pb-2 w-max">
        {{ $t('Experience') }}
      </h2>

      <div class="flex flex-col gap-8">
        <!-- Experience 1: Kreasi Hexa -->
        <div
          class="flex flex-col md:flex-row gap-4 md:gap-12 border-l-2 border-zinc-200 pl-6 md:pl-8 py-2 relative group"
        >
          <div
            class="absolute -left-[9px] top-4 w-4 h-4 rounded-full bg-white border-4 border-zinc-200 transition-colors duration-300 group-hover:border-zinc-900"
          ></div>
          <div class="md:w-1/4 text-zinc-500 font-semibold pt-1">Oct 2025 - Apr 2026</div>
          <div class="md:w-3/4">
            <h3 class="text-xl font-bold text-zinc-900 flex items-center gap-2">
              <IconBriefcase class="w-5 h-5" /> Kreasi Hexa Indonesia
            </h3>
            <p class="text-zinc-900 font-medium mb-3">Full-stack Web Developer Intern</p>

            <ul class="text-zinc-500 space-y-2 list-disc list-outside ml-4">
              <li>
                {{ $t('hexa_task_1') }}
              </li>
              <li v-html="$t('hexa_task_2')"></li>
              <li>
                {{ $t('hexa_task_3') }}
              </li>
            </ul>
          </div>
        </div>

        <!-- Experience 2: Suarga (Bangkit Capstone) -->
        <div
          class="flex flex-col md:flex-row gap-4 md:gap-12 border-l-2 border-zinc-200 pl-6 md:pl-8 py-2 relative group"
        >
          <div
            class="absolute -left-[9px] top-4 w-4 h-4 rounded-full bg-white border-4 border-zinc-200 transition-colors duration-300 group-hover:border-zinc-900"
          ></div>
          <div class="md:w-1/4 text-zinc-500 font-semibold pt-1">Apr 2024 - Jul 2024</div>
          <div class="md:w-3/4">
            <h3 class="text-xl font-bold text-zinc-900 flex items-center gap-2">
              <IconBriefcase class="w-5 h-5" /> Suarga (Bangkit Capstone Project)
            </h3>
            <p class="text-zinc-900 font-medium mb-3">Mobile Developer</p>

            <ul class="text-zinc-500 space-y-2 list-disc list-outside ml-4">
              <li v-html="$t('suarga_task_1')"></li>
              <li>{{ $t('suarga_task_2') }}</li>
              <li v-html="$t('suarga_task_3')"></li>
            </ul>
          </div>
        </div>
      </div>
    </section>

    <!-- 2. EDUCATION SECTION -->
    <section class="mb-16">
      <h2 class="text-2xl font-bold text-zinc-900 mb-8 border-b-2 border-zinc-900 pb-2 w-max">
        {{ $t('Education & Training') }}
      </h2>

      <div class="flex flex-col gap-8">
        <!-- Universitas Brawijaya -->
        <div
          class="flex flex-col md:flex-row gap-4 md:gap-12 border-l-2 border-zinc-200 pl-6 md:pl-8 py-2 relative group"
        >
          <div
            class="absolute -left-[9px] top-4 w-4 h-4 rounded-full bg-white border-4 border-zinc-200 transition-colors duration-300 group-hover:border-zinc-900"
          ></div>
          <div class="md:w-1/4 text-zinc-500 font-semibold pt-1">Aug 2021 - Jul 2025</div>
          <div class="md:w-3/4">
            <h3 class="text-xl font-bold text-zinc-900 flex items-center gap-2">
              <IconSchool class="w-5 h-5" /> Universitas Brawijaya
            </h3>
            <p class="text-zinc-900 font-medium mb-2" v-html="$t('study_program')"></p>
            <p class="text-zinc-500 leading-relaxed" v-html="$t('ub_desc')"></p>
          </div>
        </div>

        <!-- Bangkit Academy -->
        <div
          class="flex flex-col md:flex-row gap-4 md:gap-12 border-l-2 border-zinc-200 pl-6 md:pl-8 py-2 relative group"
        >
          <div
            class="absolute -left-[9px] top-4 w-4 h-4 rounded-full bg-white border-4 border-zinc-200 transition-colors duration-300 group-hover:border-zinc-900"
          ></div>
          <div class="md:w-1/4 text-zinc-500 font-semibold pt-1">Feb 2024 - Jul 2024</div>
          <div class="md:w-3/4">
            <h3 class="text-xl font-bold text-zinc-900 flex items-center gap-2">
              <IconSchool class="w-5 h-5" /> Bangkit Academy 2024 H1
            </h3>
            <p class="text-zinc-900 font-medium mb-2">Mobile Development Cohort</p>
            <p class="text-zinc-500 leading-relaxed" v-html="$t('bangkit_desc')"></p>
          </div>
        </div>
      </div>
    </section>

    <!-- 3. CERTIFICATIONS SECTION -->
    <section class="mb-24">
      <h2 class="text-2xl font-bold text-zinc-900 mb-8 border-b-2 border-zinc-900 pb-2 w-max">
        {{ $t('Certifications') }}
      </h2>

      <div class="grid grid-cols-1 md:grid-cols-2 gap-4 content-start min-h-[300px]">
        <a
          v-for="(cert, index) in paginatedCertificates"
          :key="index"
          :href="cert.link"
          target="_blank"
          rel="noopener noreferrer"
          class="p-5 border border-zinc-200 rounded-xl hover:border-zinc-900 hover:shadow-sm transition-all flex items-start gap-4 group cursor-pointer bg-white h-full"
        >
          <IconCertificate
            class="w-6 h-6 text-zinc-900 shrink-0 mt-1 transition-transform group-hover:scale-110"
          />
          <div>
            <h3
              class="font-bold text-zinc-900 group-hover:underline decoration-2 underline-offset-2"
            >
              {{ cert.title }}
            </h3>
            <p class="text-sm text-zinc-500 mb-1">Dicoding Indonesia</p>
            <span class="text-xs font-semibold text-zinc-400">{{ cert.date }}</span>
          </div>
        </a>
      </div>

      <!-- Tombol Navigasi Slider -->
      <div class="flex justify-center gap-4 mt-8">
        <button
          @click="prevPage"
          :disabled="currentPage === 0"
          class="p-2 border-2 border-zinc-200 rounded-full text-zinc-900 hover:border-zinc-900 disabled:opacity-30 disabled:hover:border-zinc-200 disabled:cursor-not-allowed transition-colors"
        >
          <IconChevronLeft class="w-6 h-6" />
        </button>
        <button
          @click="nextPage"
          :disabled="currentPage === totalPages - 1"
          class="p-2 border-2 border-zinc-200 rounded-full text-zinc-900 hover:border-zinc-900 disabled:opacity-30 disabled:hover:border-zinc-200 disabled:cursor-not-allowed transition-colors"
        >
          <IconChevronRight class="w-6 h-6" />
        </button>
      </div>
    </section>

    <!-- VIEW CV CTA -->
    <div class="mt-20 mb-12 flex justify-center">
      <a
        href="/Resume_Apriandhita.pdf"
        target="_blank"
        rel="noopener noreferrer"
        class="inline-flex items-center gap-2 px-8 py-4 bg-zinc-900 text-white rounded-full font-semibold hover:bg-zinc-800 hover:-translate-y-1 transition-all duration-300 shadow-md hover:shadow-lg"
      >
        <IconFileDescription class="w-5 h-5" />
        <span>{{ $t('view_cv') }}</span>
      </a>
    </div>
  </main>
</template>
