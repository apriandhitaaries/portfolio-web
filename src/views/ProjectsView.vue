<script setup>
import { IconBrandGithub, IconExternalLink } from '@tabler/icons-vue'

// Data Proyek
const projects = [
  {
    id: 'nontonapa',
    titleKey: 'NontonApa - Movie Review Platform',
    categoryKey: 'Full-stack Web',
    descKey: 'nontonapa_desc',
    techStack: ['Laravel', 'Vue.js', 'Tailwind CSS', 'Supabase'],
    githubUrl: 'https://github.com/apriandhitaaries/website-review-film',
    liveUrl: '#',
    hasImage: false,
  },
  {
    id: 'suarga',
    titleKey: 'Suarga - Stunting Prevention App',
    categoryKey: 'Mobile App (Android)',
    descKey: 'suarga_proj_desc',
    techStack: ['Kotlin', 'Android Studio', 'REST API'],
    githubUrl: 'https://github.com/SuargaOrgs/mobile-development',
    liveUrl: '#',
    hasImage: false,
  },
]
</script>

<template>
  <main class="max-w-7xl mx-auto px-6 md:px-12 pt-6 pb-24 min-h-screen">
    <section class="mb-16">
      <div class="mb-12 border-b-2 border-zinc-900 pb-4">
        <h1 class="text-4xl font-bold text-zinc-900 tracking-tight">
          {{ $t('Featured Projects') }}
        </h1>
        <p class="text-zinc-500 mt-2 text-lg">
          {{ $t('projects_subtitle') }}
        </p>
      </div>

      <div class="grid grid-cols-1 md:grid-cols-2 gap-8 items-start content-start min-h-[300px]">
        <div
          v-for="project in projects"
          :key="project.id"
          class="border-2 border-zinc-200 rounded-2xl p-6 md:p-8 bg-white hover:border-zinc-900 transition-all duration-300 flex flex-col justify-between h-full group"
        >
          <div>
            <div class="flex justify-between items-start mb-6 gap-4">
              <span
                class="text-xs font-bold uppercase tracking-wider px-3 py-1 bg-zinc-100 text-zinc-700 rounded-full border border-zinc-200"
              >
                {{ $t(project.categoryKey) }}
              </span>
            </div>

            <h3
              class="text-xl font-bold text-zinc-900 mb-3 group-hover:underline decoration-2 underline-offset-2"
            >
              {{ project.titleKey }}
            </h3>

            <p
              class="text-zinc-500 leading-relaxed mb-6 text-sm md:text-base"
              v-html="$t(project.descKey)"
            ></p>
          </div>

          <div>
            <div class="flex flex-wrap gap-2 mb-6">
              <span
                v-for="tech in project.techStack"
                :key="tech"
                class="text-xs font-medium text-zinc-700 bg-zinc-50 border border-zinc-200 px-2.5 py-1 rounded-md"
              >
                {{ tech }}
              </span>
            </div>

            <div class="flex items-center gap-4 pt-4 border-t border-zinc-100 mt-4">
              <a
                v-if="project.githubUrl"
                :href="project.githubUrl"
                target="_blank"
                rel="noopener noreferrer"
                class="inline-flex items-center gap-1.5 text-sm font-semibold text-zinc-600 hover:text-zinc-900 hover:-translate-y-1 transition-all duration-300"
              >
                <IconBrandGithub class="w-4 h-4" />
                <span>{{ $t('Code') }}</span>
              </a>

              <a
                v-if="project.liveUrl && project.liveUrl !== '#'"
                :href="project.liveUrl"
                target="_blank"
                rel="noopener noreferrer"
                class="inline-flex items-center gap-1.5 text-sm font-semibold text-zinc-600 hover:text-zinc-900 hover:-translate-y-1 transition-all duration-300"
              >
                <IconExternalLink class="w-4 h-4" />
                <span>{{ $t('Live Preview') }}</span>
              </a>
            </div>
          </div>
        </div>
      </div>
    </section>
  </main>
</template>
