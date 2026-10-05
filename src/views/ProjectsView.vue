<script setup>
import { ref, computed } from 'vue'
import { IconBrandGithub, IconExternalLink, IconBrandFigma } from '@tabler/icons-vue'

// Kategori Filter
const categories = ['All', 'Web Platform', 'Mobile App', 'UI/UX Design']
const selectedCategory = ref('All')

// Data Proyek
const projects = [
  {
    id: 'nontonapa',
    titleKey: 'NontonApa - Movie Review Platform',
    categoryKey: 'Web Platform',
    descKey: 'nontonapa_desc',
    techStack: ['Laravel', 'Bootstrap', 'Supabase'],
    githubUrl: 'https://github.com/apriandhitaaries/website-review-film',
    liveUrl: '#',
    hasImage: true,
    imageUrl: 'src/assets/projects/nontonapa.webp',
    bgColor: 'bg-zinc-900',
  },
  {
    id: 'suarga',
    titleKey: 'Suarga - Stunting Prevention App',
    categoryKey: 'Mobile App',
    typeMarker: 'Android Native',
    descKey: 'suarga_proj_desc',
    techStack: ['Kotlin', 'Android Studio'],
    githubUrl: 'https://github.com/SuargaOrgs/mobile-development',
    liveUrl: '#',
    hasImage: true,
    imageUrl: 'src/assets/projects/Suarga.webp',
    bgColor: 'bg-emerald-100',
  },
  {
    id: 'dicoding-story',
    titleKey: 'Dicoding Story App',
    categoryKey: 'Mobile App',
    typeMarker: 'Android Native',
    descKey: 'story_app_desc',
    techStack: ['Kotlin', 'Android Studio'],
    githubUrl: 'https://github.com/apriandhitaaries/What_Your_Story',
    liveUrl: '',
    hasImage: true,
    imageUrl: 'src/assets/projects/dicoding_story.webp',
    bgColor: 'bg-blue-100',
  },
  // {
  //   id: 'cancer-detection',
  //   titleKey: 'Cancer Detection',
  //   categoryKey: 'Mobile App',
  //   typeMarker: 'Android Native',
  //   descKey: 'story_app_desc',
  //   techStack: ['Kotlin', 'Android Studio'],
  //   githubUrl: 'https://github.com/apriandhitaaries/Cancer_Detection',
  //   liveUrl: '',
  //   hasImage: true,
  //   imageUrl: 'src/assets/projects/dicoding_story.webp',
  //   bgColor: 'bg-blue-100',
  // },
  // {
  //   id: 'github-user-search',
  //   titleKey: 'Github User Search',
  //   categoryKey: 'Mobile App',
  //   typeMarker: 'Android Native',
  //   descKey: 'story_app_desc',
  //   techStack: ['Kotlin', 'Android Studio'],
  //   githubUrl: 'https://github.com/apriandhitaaries/GitHubUserSearch',
  //   liveUrl: '',
  //   hasImage: true,
  //   imageUrl: 'src/assets/projects/dicoding_story.webp',
  //   bgColor: 'bg-blue-100',
  // },
  {
    id: 'kenali-oshimu',
    titleKey: 'Kenali Oshimu',
    categoryKey: 'Mobile App',
    typeMarker: 'Android Native',
    descKey: 'kenali_oshimu_desc',
    techStack: ['Kotlin', 'Android Studio'],
    githubUrl: 'https://github.com/apriandhitaaries/Kenali_Oshimu',
    liveUrl: '',
    hasImage: true,
    imageUrl: 'src/assets/projects/kenali-oshimu.webp',
    bgColor: 'bg-blue-100',
  },
  {
    id: 'medease',
    titleKey: 'MedEase - Healthcare Registration',
    categoryKey: 'Web Platform',
    descKey: 'medease_desc',
    techStack: ['Laravel', 'Bootstrap'],
    githubUrl: 'https://github.com/apriandhitaaries/MedEase',
    liveUrl: '',
    hasImage: true,
    imageUrl: 'src/assets/projects/medease.webp',
    bgColor: 'bg-teal-50',
  },
  {
    id: 'learnbycode',
    titleKey: 'LearnByCode',
    categoryKey: 'UI/UX Design',
    descKey: 'learnbycode_desc',
    techStack: ['Figma', 'Wireframing', 'Prototyping'],
    githubUrl: '',
    figmaUrl: 'https://www.figma.com/proto/2n794eCepFTrZ8Q5oPZ2UT/Learn-By-Code-DPB?page-id=481%3A815&node-id=481-817&starting-point-node-id=481%3A817&t=SpkFpdira7Yd8sgn-1',
    liveUrl: '',
    hasImage: true,
    imageUrl: 'src/assets/projects/learnbycode.webp',
    bgColor: 'bg-indigo-900',
  },
]

const filteredProjects = computed(() => {
  if (selectedCategory.value === 'All') return projects
  return projects.filter(p => p.categoryKey === selectedCategory.value)
})
</script>

<template>
  <main class="max-w-7xl mx-auto px-6 md:px-12 pt-6 pb-24 min-h-screen">
    <section class="mb-16">
      <div class="mb-8 border-b-2 border-zinc-900 pb-4">
        <h1 class="text-4xl font-bold text-zinc-900 tracking-tight">
          {{ $t('Featured Projects') }}
        </h1>
        <p class="text-zinc-500 mt-2 text-lg">
          {{ $t('projects_subtitle') }}
        </p>
      </div>

      <!-- Filter Buttons -->
      <div class="flex flex-wrap gap-3 mb-10">
        <button
          v-for="cat in categories"
          :key="cat"
          @click="selectedCategory = cat"
          :class="[
            'px-5 py-2 rounded-full text-sm font-semibold transition-all duration-300',
            selectedCategory === cat
              ? 'bg-zinc-900 text-white shadow-md'
              : 'bg-zinc-100 text-zinc-600 hover:bg-zinc-200 hover:text-zinc-900'
          ]"
        >
          {{ $t(cat) }}
        </button>
      </div>

      <div class="grid grid-cols-1 md:grid-cols-2 gap-8 items-start content-start min-h-[300px]">
        <div
          v-for="project in filteredProjects"
          :key="project.id"
          class="border-2 border-zinc-200 rounded-2xl bg-white hover:border-zinc-900 transition-all duration-300 flex flex-col h-full group overflow-hidden"
        >
          <!-- Image Section -->
          <div v-if="project.hasImage" :class="['w-full aspect-video relative flex items-center justify-center overflow-hidden border-b-2 border-zinc-200 group-hover:border-zinc-900 transition-colors duration-300', project.bgColor]">
            <img
              :src="project.imageUrl"
              :alt="project.titleKey"
              class="w-full h-full object-cover object-top group-hover:scale-105 transition-all duration-500"
            />
          </div>

          <div class="p-6 md:p-8 flex flex-col justify-between flex-grow">
            <div>
            <div class="flex flex-wrap items-start mb-6 gap-2">
              <span
                class="text-xs font-bold uppercase tracking-wider px-3 py-1 bg-zinc-100 text-zinc-700 rounded-full border border-zinc-200"
              >
                {{ $t(project.categoryKey) }}
              </span>
              <span
                v-if="project.typeMarker"
                class="text-xs font-bold uppercase tracking-wider px-3 py-1 bg-emerald-100 text-emerald-800 rounded-full border border-emerald-200"
              >
                {{ project.typeMarker }}
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
                v-if="project.figmaUrl"
                :href="project.figmaUrl"
                target="_blank"
                rel="noopener noreferrer"
                class="inline-flex items-center gap-1.5 text-sm font-semibold text-zinc-600 hover:text-purple-600 hover:-translate-y-1 transition-all duration-300"
              >
                <IconBrandFigma class="w-4 h-4 text-purple-600" />
                <span>{{ $t('Figma Prototype') }}</span>
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
      </div>
    </section>
  </main>
</template>
