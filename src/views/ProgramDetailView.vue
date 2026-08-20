<script setup>
import { computed } from 'vue'
import { useRoute, useRouter } from 'vue-router'
import { programData } from '../data/program'
import { ArrowLeft, Clock, Calendar, User, Tag, Sparkles, Share2, CheckCircle2, ArrowRight } from 'lucide-vue-next'

const props = defineProps({
  slug: String
})

const route = useRoute()
const router = useRouter()

const currentSlug = computed(() => props.slug || route.params.slug)

const program = computed(() => {
  return programData.find(p => p.slug === currentSlug.value)
})

const otherPrograms = computed(() => {
  return programData.filter(p => p.slug !== currentSlug.value).slice(0, 3)
})

const navigateTo = (path) => {
  router.push(path)
}
</script>

<template>
  <div class="pt-24 pb-20 bg-[#FAFAFA] min-h-screen">
    <div class="max-w-[1180px] mx-auto px-5 sm:px-6">
      
      <!-- Back Navigation & Breadcrumb -->
      <div class="flex flex-wrap items-center justify-between gap-4 mb-8">
        <button
          @click="router.push('/')"
          class="inline-flex items-center gap-2 text-xs sm:text-sm font-bold text-[#0056C2] hover:text-[#003E8F] bg-white px-4 py-2 rounded-xl border border-[#E5E7EB] shadow-subtle transition-smooth cursor-pointer"
        >
          <ArrowLeft class="w-4 h-4" />
          <span>Kembali ke Beranda</span>
        </button>

        <nav class="flex items-center gap-2 text-xs text-[#4B5563] font-medium">
          <router-link to="/" class="hover:text-[#0056C2]">Beranda</router-link>
          <span>/</span>
          <a href="/#program" @click.prevent="router.push({ path: '/', hash: '#program' })" class="hover:text-[#0056C2]">Program</a>
          <span>/</span>
          <span class="text-[#0B0F19] font-bold truncate max-w-[200px] sm:max-w-none">{{ program?.title }}</span>
        </nav>
      </div>

      <!-- 404 Fallback if Program Not Found -->
      <div v-if="!program" class="bg-white rounded-3xl p-12 border border-[#E5E7EB] text-center max-w-lg mx-auto shadow-subtle">
        <h2 class="text-2xl font-bold text-[#0B0F19] mb-2">Program Tidak Ditemukan</h2>
        <p class="text-sm text-[#4B5563] mb-6">Program pengabdian yang Anda cari tidak tersedia atau telah dipindahkan.</p>
        <button @click="router.push('/')" class="px-6 py-3 bg-[#0056C2] text-white text-sm font-bold rounded-xl shadow-subtle">
          Kembali ke Beranda
        </button>
      </div>

      <!-- Main Article View -->
      <div v-else class="grid grid-cols-1 lg:grid-cols-12 gap-10">
        
        <!-- Left: Article Content Body (8 Cols) -->
        <main class="lg:col-span-8 bg-white rounded-3xl p-6 sm:p-10 border border-[#E5E7EB] shadow-subtle">
          
          <!-- Category & SDGs Badges -->
          <div class="flex flex-wrap items-center gap-2.5 mb-4">
            <span class="px-3.5 py-1 rounded-full bg-[#EAF3FF] text-[#0056C2] text-xs font-bold uppercase tracking-wider">
              {{ program.categoryLabel }}
            </span>
            <span class="px-3.5 py-1 rounded-full bg-[#FAFAFA] text-[#0B0F19] border border-[#E5E7EB] text-xs font-bold">
              {{ program.sdgs }}
            </span>
          </div>

          <!-- Title -->
          <h1 class="text-2xl sm:text-4xl font-extrabold text-[#0B0F19] tracking-tight leading-tight mb-4">
            {{ program.title }}
          </h1>

          <!-- Meta Author & Date -->
          <div class="flex flex-wrap items-center gap-4 text-xs text-[#4B5563] font-medium pb-6 border-b border-[#E5E7EB] mb-6">
            <div class="flex items-center gap-1.5">
              <User class="w-4 h-4 text-[#0056C2]" />
              <span>{{ program.author || 'Tim Komunikasi UNBITA' }}</span>
            </div>
            <div class="flex items-center gap-1.5">
              <Calendar class="w-4 h-4 text-[#0056C2]" />
              <span>{{ program.date || '20 Agustus 2026' }}</span>
            </div>
            <div class="flex items-center gap-1.5">
              <Clock class="w-4 h-4 text-[#0056C2]" />
              <span>{{ program.readTime || '5 Menit Baca' }}</span>
            </div>
          </div>

          <!-- Featured Header Image -->
          <div class="relative aspect-[16/9] rounded-2xl overflow-hidden mb-8 border border-[#E5E7EB] bg-[#FAFAFA]">
            <img :src="program.image" :alt="program.title" class="w-full h-full object-cover" />
          </div>

          <!-- Summary Callout -->
          <div class="p-5 bg-[#EAF3FF] border-l-4 border-[#0056C2] rounded-r-2xl mb-8">
            <p class="text-sm sm:text-base font-semibold text-[#0056C2] leading-relaxed m-0">
              {{ program.summary }}
            </p>
          </div>

          <!-- HTML Rendered Article Body Content -->
          <div class="article-body-content" v-html="program.descriptionHtml"></div>

        </main>

        <!-- Right: Sidebar Information & Quick Actions (4 Cols) -->
        <aside class="lg:col-span-4 space-y-6">
          
          <!-- Program Quick Specs Box -->
          <div class="bg-white rounded-3xl p-6 border border-[#E5E7EB] shadow-subtle space-y-4">
            <h3 class="text-base font-bold text-[#0B0F19] pb-3 border-b border-[#E5E7EB]">
              Ringkasan Program
            </h3>

            <div class="space-y-3 text-xs">
              <div class="flex justify-between items-center py-1">
                <span class="text-[#4B5563]">Kategori</span>
                <span class="font-bold text-[#0B0F19]">{{ program.categoryLabel }}</span>
              </div>
              <div class="flex justify-between items-center py-1">
                <span class="text-[#4B5563]">Target SDGs</span>
                <span class="font-bold text-[#0056C2]">{{ program.sdgs }}</span>
              </div>
              <div class="flex justify-between items-center py-1">
                <span class="text-[#4B5563]">Lokasi Pengabdian</span>
                <span class="font-bold text-[#0B0F19]">9 Kecamatan</span>
              </div>
              <div class="flex justify-between items-center py-1">
                <span class="text-[#4B5563]">Instansi</span>
                <span class="font-bold text-[#0B0F19]">UNBITA Gorontalo</span>
              </div>
            </div>

            <div class="pt-3 border-t border-[#E5E7EB]">
              <a
                href="#wilayah"
                @click.prevent="router.push('/#wilayah')"
                class="w-full py-3 bg-[#0056C2] hover:bg-[#003E8F] text-white text-xs font-bold rounded-xl flex items-center justify-center gap-2 transition-smooth cursor-pointer shadow-subtle"
              >
                <span>Lihat Sebaran Wilayah</span>
                <ArrowRight class="w-4 h-4" />
              </a>
            </div>
          </div>

          <!-- Other Programs Recommendations -->
          <div class="bg-white rounded-3xl p-6 border border-[#E5E7EB] shadow-subtle space-y-4">
            <h3 class="text-base font-bold text-[#0B0F19] pb-3 border-b border-[#E5E7EB]">
              Program Lainnya
            </h3>

            <div class="space-y-4">
              <div
                v-for="item in otherPrograms"
                :key="item.id"
                @click="navigateTo(`/program/${item.slug}`)"
                class="group flex items-start gap-3 cursor-pointer"
              >
                <div class="w-16 h-16 rounded-xl overflow-hidden bg-[#FAFAFA] flex-shrink-0 border border-[#E5E7EB]">
                  <img :src="item.image" :alt="item.title" class="w-full h-full object-cover group-hover:scale-105 transition-transform" />
                </div>
                <div>
                  <span class="text-[10px] font-bold text-[#0056C2] uppercase block">{{ item.categoryLabel }}</span>
                  <h4 class="text-xs font-bold text-[#0B0F19] group-hover:text-[#0056C2] transition-colors leading-snug line-clamp-2">
                    {{ item.title }}
                  </h4>
                </div>
              </div>
            </div>
          </div>

        </aside>

      </div>

    </div>
  </div>
</template>

<style>
/* Styling for Rich HTML Content */
.article-body-content {
  color: #0B0F19;
  font-size: 0.95rem;
  line-height: 1.75;
}

.article-body-content p {
  margin-bottom: 1.25rem;
  color: #4B5563;
}

.article-body-content p.lead-paragraph {
  font-size: 1.05rem;
  font-weight: 500;
  color: #0B0F19;
  line-height: 1.7;
}

.article-body-content h2 {
  font-size: 1.35rem;
  font-weight: 800;
  color: #0B0F19;
  margin-top: 2rem;
  margin-bottom: 0.75rem;
  letter-spacing: -0.02em;
}

.article-body-content h3 {
  font-size: 1.15rem;
  font-weight: 700;
  color: #0B0F19;
  margin-top: 1.5rem;
  margin-bottom: 0.5rem;
}

.article-body-content ul, .article-body-content ol {
  margin-bottom: 1.5rem;
  padding-left: 1.25rem;
}

.article-body-content ul {
  list-style-type: disc;
}

.article-body-content ol {
  list-style-type: decimal;
}

.article-body-content li {
  margin-bottom: 0.5rem;
  color: #4B5563;
}

.article-body-content blockquote {
  border-left: 4px solid #0056C2;
  padding-left: 1.25rem;
  margin: 1.75rem 0;
  font-style: italic;
  font-weight: 600;
  color: #0B0F19;
  font-size: 1.05rem;
}
</style>
