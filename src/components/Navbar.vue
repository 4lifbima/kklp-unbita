<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import { Menu, X, ArrowRight } from 'lucide-vue-next'

const isScrolled = ref(false)
const isMobileMenuOpen = ref(false)

const navLinks = [
  { name: 'Home', href: '#hero' },
  { name: 'Tentang', href: '#tentang' },
  { name: 'Wilayah', href: '#wilayah' },
  { name: 'Program', href: '#program' },
  { name: 'Kegiatan', href: '#kegiatan' },
]

const handleScroll = () => {
  isScrolled.value = window.scrollY > 15
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})

const scrollTo = (href) => {
  isMobileMenuOpen.value = false
  const element = document.querySelector(href)
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' })
  }
}
</script>

<template>
  <header
    class="fixed top-0 left-0 right-0 z-40 transition-smooth"
    :class="[
      isScrolled
        ? 'bg-white border-b border-[#E5E7EB] shadow-subtle py-3'
        : 'bg-white border-b border-[#E5E7EB] py-4'
    ]"
  >
    <div class="max-w-[1180px] mx-auto px-5 sm:px-6 flex items-center justify-between">
      
      <!-- Brand Logo -->
      <a href="#hero" @click.prevent="scrollTo('#hero')" class="flex items-center gap-3 group text-decoration-none">
        <div class="flex items-center justify-center transition-smooth">
          <img src="/images/logo-unbita.png" alt="Logo UNBITA" class="w-10 h-10 object-contain">
        </div>
        <div class="flex flex-col">
          <span class="text-lg sm:text-xl font-extrabold tracking-tight text-[#0056C2] leading-none">
            KKLP <span class="text-[#0B0F19]">UNBITA</span>
          </span>
          <span class="text-[8px] sm:text-[11px] font-bold text-[#4B5563] tracking-widest uppercase mt-0.5">
            Universitas Bina Taruna Gorontalo
          </span>
        </div>
      </a>

      <!-- Desktop Nav Links -->
      <nav class="hidden md:flex items-center gap-8">
        <a
          v-for="link in navLinks"
          :key="link.name"
          :href="link.href"
          @click.prevent="scrollTo(link.href)"
          class="text-sm font-semibold text-[#4B5563] hover:text-[#0056C2] transition-smooth relative py-1 hover:before:w-full before:w-0 before:h-0.5 before:bg-[#0056C2] before:absolute before:bottom-0 before:left-0 before:transition-all"
        >
          {{ link.name }}
        </a>
      </nav>

      <!-- CTA & Mobile Toggle -->
      <div class="flex items-center gap-3">
        <a
          href="#program"
          @click.prevent="scrollTo('#program')"
          class="hidden sm:inline-flex items-center gap-2 px-5 py-2.5 bg-[#0056C2] hover:bg-[#003E8F] text-white font-bold text-sm rounded-xl transition-smooth shadow-subtle cursor-pointer"
        >
          <span>Lihat Program</span>
          <ArrowRight class="w-4 h-4" />
        </a>

        <!-- Mobile Menu Toggle -->
        <button
          @click="isMobileMenuOpen = !isMobileMenuOpen"
          class="md:hidden p-2 rounded-xl text-[#0B0F19] hover:bg-[#F8FAFC] border border-[#E5E7EB] transition-smooth"
          aria-label="Toggle navigation menu"
        >
          <Menu v-if="!isMobileMenuOpen" class="w-6 h-6" />
          <X v-else class="w-6 h-6" />
        </button>
      </div>
    </div>

    <!-- Mobile Drawer -->
    <transition
      enter-active-class="transition duration-200 ease-out"
      enter-from-class="opacity-0 -translate-y-2"
      enter-to-class="opacity-100 translate-y-0"
      leave-active-class="transition duration-150 ease-in"
      leave-from-class="opacity-100 translate-y-0"
      leave-to-class="opacity-0 -translate-y-2"
    >
      <div
        v-if="isMobileMenuOpen"
        class="md:hidden bg-white border-b border-[#E5E7EB] px-5 py-6 shadow-card"
      >
        <div class="flex flex-col gap-4">
          <a
            v-for="link in navLinks"
            :key="link.name"
            :href="link.href"
            @click.prevent="scrollTo(link.href)"
            class="text-base font-bold text-[#0B0F19] hover:text-[#0056C2] py-2 border-b border-[#F8FAFC]"
          >
            {{ link.name }}
          </a>
          <a
            href="#program"
            @click.prevent="scrollTo('#program')"
            class="mt-2 w-full flex items-center justify-center gap-2 px-5 py-3 bg-[#0056C2] text-white font-bold rounded-xl text-center shadow-subtle"
          >
            <span>Lihat Program KKLP</span>
            <ArrowRight class="w-4 h-4" />
          </a>
        </div>
      </div>
    </transition>
  </header>
</template>
