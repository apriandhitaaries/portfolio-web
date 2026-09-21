<script setup>
import { ref } from 'vue'
import { useI18n } from 'vue-i18n'
// Menggunakan ikon dari Tabler Icons untuk tampilan yang konsisten dan rapi
import { IconLanguage, IconCheck, IconMenu2, IconX } from '@tabler/icons-vue'

const isMenuOpen = ref(false)
const isLangMenuOpen = ref(false)
const { locale } = useI18n()

// PENJELASAN: Variabel activeMenu SUDAH DIHAPUS.
// Dengan Vue Router, kita tidak perlu melacak menu yang aktif secara manual.
// Kita akan mengecek status aktif langsung dari URL ($route.path).

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value
}

const toggleLangMenu = () => {
  isLangMenuOpen.value = !isLangMenuOpen.value
}

const setLanguage = (lang) => {
  locale.value = lang
  isLangMenuOpen.value = false
}
</script>

<template>
  <header
    class="w-full bg-white/90 backdrop-blur-md fixed top-0 z-50 border-b border-zinc-100 transition-all"
  >
    <nav
      class="max-w-7xl mx-auto flex justify-between items-center py-5 px-6 md:px-12 relative z-50"
    >
      <RouterLink
        to="/"
        class="font-extrabold text-2xl tracking-tighter text-zinc-900 hover:opacity-80 transition-opacity"
      >
        APRIANDHITA.
      </RouterLink>

      <div class="hidden md:flex items-center gap-6 font-medium text-sm uppercase tracking-widest">
        <RouterLink
          to="/about"
          :class="
            $route.path === '/about'
              ? 'text-zinc-900 font-extrabold border-b-2 border-zinc-900'
              : 'text-zinc-500 font-semibold border-b-2 border-transparent hover:text-zinc-900 hover:border-zinc-300'
          "
          class="pb-1 transition-all duration-300"
        >
          {{ $t('About') }}
        </RouterLink>

        <RouterLink
          to="/projects"
          :class="
            $route.path === '/projects'
              ? 'text-zinc-900 font-extrabold border-b-2 border-zinc-900'
              : 'text-zinc-500 font-semibold border-b-2 border-transparent hover:text-zinc-900 hover:border-zinc-300'
          "
          class="pb-1 transition-all duration-300"
        >
          {{ $t('Projects') }}
        </RouterLink>

        <RouterLink
          to="/contact"
          :class="
            $route.path === '/contact'
              ? 'text-zinc-900 font-extrabold border-b-2 border-zinc-900'
              : 'text-zinc-500 font-semibold border-b-2 border-transparent hover:text-zinc-900 hover:border-zinc-300'
          "
          class="pb-1 transition-all duration-300"
        >
          {{ $t('Contact') }}
        </RouterLink>

        <div class="h-4 w-px bg-zinc-300 mx-2"></div>

        <div class="relative">
          <button
            @click="toggleLangMenu"
            class="flex items-center gap-1 pb-1 font-bold transition-all duration-300 focus:outline-none border-b-2"
            :class="
              isLangMenuOpen
                ? 'text-zinc-900 border-zinc-900'
                : 'text-zinc-500 border-transparent hover:text-zinc-900 hover:border-zinc-300'
            "
          >
            <IconLanguage class="w-5 h-5" />
            {{ locale === 'en' ? 'EN' : 'ID' }}
          </button>

          <transition
            enter-active-class="transition duration-200 ease-out"
            enter-from-class="opacity-0 translate-y-2"
            enter-to-class="opacity-100 translate-y-0"
            leave-active-class="transition duration-150 ease-in"
            leave-from-class="opacity-100 translate-y-0"
            leave-to-class="opacity-0 translate-y-2"
          >
            <div
              v-show="isLangMenuOpen"
              class="absolute right-0 mt-2 w-44 bg-white border border-zinc-100 rounded-xl shadow-lg z-50"
            >
              <div class="p-2 flex flex-col gap-1">
                <button
                  @click="setLanguage('en')"
                  :class="
                    locale === 'en'
                      ? 'bg-zinc-900 text-white'
                      : 'text-zinc-600 hover:bg-zinc-50 hover:text-zinc-900'
                  "
                  class="flex items-center justify-between w-full px-3 py-2.5 text-sm font-bold rounded-lg transition-colors"
                >
                  <div class="flex items-center gap-3">
                    <span
                      :class="locale === 'en' ? 'bg-white/20' : 'bg-zinc-100'"
                      class="px-1.5 py-0.5 rounded text-[10px]"
                      >EN</span
                    >
                    English
                  </div>
                  <IconCheck v-if="locale === 'en'" class="w-4 h-4" />
                </button>

                <button
                  @click="setLanguage('id')"
                  :class="
                    locale === 'id'
                      ? 'bg-zinc-900 text-white'
                      : 'text-zinc-600 hover:bg-zinc-50 hover:text-zinc-900'
                  "
                  class="flex items-center justify-between w-full px-3 py-2.5 text-sm font-bold rounded-lg transition-colors"
                >
                  <div class="flex items-center gap-3">
                    <span
                      :class="locale === 'id' ? 'bg-white/20' : 'bg-zinc-100'"
                      class="px-1.5 py-0.5 rounded text-[10px]"
                      >ID</span
                    >
                    Indonesia
                  </div>
                  <IconCheck v-if="locale === 'id'" class="w-4 h-4" />
                </button>
              </div>
            </div>
          </transition>
        </div>
      </div>

      <button
        @click="toggleMenu"
        class="md:hidden text-zinc-900 focus:outline-none p-2 rounded-lg transition-colors z-50 relative"
      >
        <IconMenu2 v-if="!isMenuOpen" class="w-6 h-6" />
        <IconX v-else class="w-6 h-6" />
      </button>
    </nav>

    <transition
      enter-active-class="transition-opacity duration-300"
      enter-from-class="opacity-0"
      enter-to-class="opacity-100"
      leave-active-class="transition-opacity duration-200"
      leave-from-class="opacity-100"
      leave-to-class="opacity-0"
    >
      <div
        v-if="isMenuOpen"
        @click="isMenuOpen = false"
        class="md:hidden absolute top-full left-0 w-full h-screen bg-zinc-900/20 backdrop-blur-sm z-40"
      ></div>
    </transition>

    <transition
      enter-active-class="transition duration-300 ease-out origin-top"
      enter-from-class="opacity-0 -translate-y-4 scale-y-95"
      enter-to-class="opacity-100 translate-y-0 scale-y-100"
      leave-active-class="transition duration-200 ease-in origin-top"
      leave-from-class="opacity-100 translate-y-0 scale-y-100"
      leave-to-class="opacity-0 -translate-y-4 scale-y-95"
    >
      <div
        v-show="isMenuOpen"
        class="md:hidden absolute top-full left-0 w-full bg-white border-b border-zinc-100 shadow-xl flex flex-col px-6 py-6 max-h-[80vh] overflow-y-auto -mt-px z-50"
      >
        <div class="flex flex-col gap-6 text-xl mb-10 mt-4 px-2">
          <RouterLink
            to="/"
            @click="isMenuOpen = false"
            class="transition-all duration-300 w-max pb-1"
            :class="
              $route.path === '/'
                ? 'text-zinc-900 font-extrabold border-b-2 border-zinc-900'
                : 'text-zinc-500 font-semibold hover:text-zinc-900'
            "
          >
            {{ $t('Home') }}
          </RouterLink>

          <RouterLink
            to="/about"
            @click="isMenuOpen = false"
            class="transition-all duration-300 w-max pb-1"
            :class="
              $route.path === '/about'
                ? 'text-zinc-900 font-extrabold border-b-2 border-zinc-900'
                : 'text-zinc-500 font-semibold hover:text-zinc-900'
            "
          >
            {{ $t('About') }}
          </RouterLink>

          <RouterLink
            to="/projects"
            @click="isMenuOpen = false"
            class="transition-all duration-300 w-max pb-1"
            :class="
              $route.path === '/projects'
                ? 'text-zinc-900 font-extrabold border-b-2 border-zinc-900'
                : 'text-zinc-500 font-semibold hover:text-zinc-900'
            "
          >
            {{ $t('Projects') }}
          </RouterLink>

          <RouterLink
            to="/contact"
            @click="isMenuOpen = false"
            class="transition-all duration-300 w-max pb-1"
            :class="
              $route.path === '/contact'
                ? 'text-zinc-900 font-extrabold border-b-2 border-zinc-900'
                : 'text-zinc-500 font-semibold hover:text-zinc-900'
            "
          >
            {{ $t('Contact') }}
          </RouterLink>
        </div>

        <div class="flex gap-3">
          <button
            @click="setLanguage('en')"
            :class="
              locale === 'en'
                ? 'border-zinc-900 text-zinc-900'
                : 'border-zinc-200 text-zinc-500 hover:border-zinc-400'
            "
            class="flex-1 bg-white border-2 py-3 rounded-xl text-sm font-bold transition-colors"
          >
            EN English
          </button>
          <button
            @click="setLanguage('id')"
            :class="
              locale === 'id'
                ? 'border-zinc-900 text-zinc-900'
                : 'border-zinc-200 text-zinc-500 hover:border-zinc-400'
            "
            class="flex-1 bg-white border-2 py-3 rounded-xl text-sm font-bold transition-colors"
          >
            ID Indonesia
          </button>
        </div>
      </div>
    </transition>
  </header>

  <div class="h-20 md:h-24"></div>
</template>
