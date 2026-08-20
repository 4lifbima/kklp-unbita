<script setup>
import { computed } from 'vue'
import { useRoute, useRouter } from 'vue-router'
import { wilayahData } from '../data/wilayah'
import { ArrowLeft, MapPin, Users, Building, ArrowRight } from 'lucide-vue-next'

const props = defineProps({
  slug: String
})

const route = useRoute()
const router = useRouter()

const currentSlug = computed(() => props.slug || route.params.slug)

const wilayah = computed(() => {
  return wilayahData.find(w => w.slug === currentSlug.value)
})

const otherWilayah = computed(() => {
  return wilayahData.filter(w => w.slug !== currentSlug.value).slice(0, 4)
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
          <a href="/#wilayah" @click.prevent="router.push({ path: '/', hash: '#wilayah' })" class="hover:text-[#0056C2]">Wilayah</a>
          <span>/</span>
          <span class="text-[#0B0F19] font-bold truncate max-w-[200px] sm:max-w-none">Kecamatan {{ wilayah?.name }}</span>
        </nav>
      </div>

      <!-- 404 Fallback -->
      <div v-if="!wilayah" class="bg-white rounded-3xl p-12 border border-[#E5E7EB] text-center max-w-lg mx-auto shadow-subtle">
        <h2 class="text-2xl font-bold text-[#0B0F19] mb-2">Wilayah Tidak Ditemukan</h2>
        <p class="text-sm text-[#4B5563] mb-6">Data kecamatan yang Anda cari tidak tersedia.</p>
        <button @click="router.push('/')" class="px-6 py-3 bg-[#0056C2] text-white text-sm font-bold rounded-xl shadow-subtle">
          Kembali ke Beranda
        </button>
      </div>

      <!-- Main Article & Details View -->
      <div v-else class="grid grid-cols-1 lg:grid-cols-12 gap-10">
        
        <!-- Left Column: Rich Content (8 Cols) -->
        <main class="lg:col-span-8 bg-white rounded-3xl p-6 sm:p-10 border border-[#E5E7EB] shadow-subtle">
          
          <!-- Badges -->
          <div class="flex flex-wrap items-center gap-2.5 mb-4">
            <span class="px-3.5 py-1 rounded-full bg-[#EAF3FF] text-[#0056C2] text-xs font-bold uppercase tracking-wider">
              Kecamatan {{ wilayah.name }}
            </span>
            <span class="px-3.5 py-1 rounded-full bg-[#FAFAFA] text-[#0B0F19] border border-[#E5E7EB] text-xs font-bold">
              Kota Gorontalo
            </span>
          </div>

          <!-- Title -->
          <h1 class="text-3xl sm:text-4xl font-extrabold text-[#0B0F19] tracking-tight leading-tight mb-4">
            Pengabdian KKLP di Kecamatan {{ wilayah.name }}
          </h1>

          <!-- Featured Image -->
          <div class="relative aspect-[16/9] rounded-2xl overflow-hidden mb-8 border border-[#E5E7EB] bg-[#FAFAFA]">
            <img :src="wilayah.image" :alt="wilayah.name" class="w-full h-full object-cover" />
          </div>

          <!-- Highlight Key Stats Bar -->
          <div class="grid grid-cols-2 sm:grid-cols-3 gap-4 p-5 bg-[#FAFAFA] border border-[#E5E7EB] rounded-2xl mb-8">
            <div>
              <span class="text-[11px] text-[#4B5563] font-semibold uppercase block">Jumlah Kelurahan</span>
              <span class="text-xl font-extrabold text-[#0B0F19]">{{ wilayah.kelurahanCount }} Kelurahan</span>
            </div>
            <div>
              <span class="text-[11px] text-[#4B5563] font-semibold uppercase block">Alokasi Mahasiswa</span>
              <span class="text-xl font-extrabold text-[#0056C2]">{{ wilayah.students }}</span>
            </div>
            <div class="col-span-2 sm:col-span-1">
              <span class="text-[11px] text-[#4B5563] font-semibold uppercase block">Instansi</span>
              <span class="text-sm font-bold text-[#0B0F19]">UNBITA Gorontalo</span>
            </div>
          </div>

          <!-- Kelurahan List Chips -->
          <div class="mb-8 p-6 bg-white border border-[#E5E7EB] rounded-2xl shadow-subtle">
            <h3 class="text-sm font-bold text-[#0B0F19] uppercase tracking-wider mb-3 flex items-center gap-2">
              <MapPin class="w-4 h-4 text-[#0056C2]" />
              <span>Daftar Kelurahan Lokasi Pengabdian ({{ wilayah.kelurahanCount }} Kelurahan)</span>
            </h3>
            <div class="flex flex-wrap gap-2">
              <span
                v-for="kel in wilayah.kelurahanList"
                :key="kel"
                class="px-3.5 py-1.5 bg-[#EAF3FF] text-[#0056C2] rounded-xl text-xs font-bold border border-[#0056C2]/20"
              >
                Kelurahan {{ kel }}
              </span>
            </div>
          </div>

          <!-- Summary Callout -->
          <div class="p-5 bg-[#EAF3FF] border-l-4 border-[#0056C2] rounded-r-2xl mb-8">
            <p class="text-sm sm:text-base font-semibold text-[#0056C2] leading-relaxed m-0">
              {{ wilayah.summary }}
            </p>
          </div>

          <!-- HTML Rendered Content -->
          <div class="article-body-content" v-html="wilayah.descriptionHtml"></div>

        </main>

        <!-- Right Column: Sidebar (4 Cols) -->
        <aside class="lg:col-span-4 space-y-6">
          
          <!-- Quick Specs Box -->
          <div class="bg-white rounded-3xl p-6 border border-[#E5E7EB] shadow-subtle space-y-4">
            <h3 class="text-base font-bold text-[#0B0F19] pb-3 border-b border-[#E5E7EB]">
              Fokus Pengabdian
            </h3>
            <p class="text-xs text-[#4B5563] leading-relaxed">
              {{ wilayah.focus }}
            </p>
            <div class="pt-2">
              <a
                href="#program"
                @click.prevent="router.push('/#program')"
                class="w-full py-3 bg-[#0056C2] hover:bg-[#003E8F] text-white text-xs font-bold rounded-xl flex items-center justify-center gap-2 transition-smooth cursor-pointer shadow-subtle"
              >
                <span>Lihat Semua Program</span>
                <ArrowRight class="w-4 h-4" />
              </a>
            </div>
          </div>

          <!-- Other Kecamatan Recommendations -->
          <div class="bg-white rounded-3xl p-6 border border-[#E5E7EB] shadow-subtle space-y-4">
            <h3 class="text-base font-bold text-[#0B0F19] pb-3 border-b border-[#E5E7EB]">
              Kecamatan Lainnya
            </h3>

            <div class="space-y-3">
              <div
                v-for="item in otherWilayah"
                :key="item.id"
                @click="navigateTo(`/wilayah/${item.slug}`)"
                class="p-3 bg-[#FAFAFA] hover:bg-[#EAF3FF] border border-[#E5E7EB] rounded-2xl cursor-pointer transition-smooth group flex items-center justify-between"
              >
                <div>
                  <h4 class="text-xs font-bold text-[#0B0F19] group-hover:text-[#0056C2] transition-colors">
                    Kecamatan {{ item.name }}
                  </h4>
                  <span class="text-[10px] text-[#4B5563]">{{ item.kelurahanCount }} Kelurahan • {{ item.students }}</span>
                </div>
                <ArrowRight class="w-4 h-4 text-[#0056C2] group-hover:translate-x-1 transition-transform" />
              </div>
            </div>
          </div>

        </aside>

      </div>

    </div>
  </div>
</template>
