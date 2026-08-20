<script setup>
import { useRouter } from 'vue-router'
import { wilayahData } from '../data/wilayah'
import { MapPin, ArrowUpRight, Compass } from 'lucide-vue-next'

const router = useRouter()

const props = defineProps({
  onSelectKecamatan: Function
})

const popularList = wilayahData.slice(0, 4)

const handleCardClick = (kec) => {
  if (props.onSelectKecamatan) {
    props.onSelectKecamatan(kec)
  } else if (kec.slug) {
    router.push(`/wilayah/${kec.slug}`)
  }
}
</script>

<template>
  <section class="py-16 md:py-24 bg-white border-y border-[#E5E7EB]">
    <div class="max-w-[1180px] mx-auto px-5 sm:px-6">
      
      <!-- Section Header -->
      <div class="flex flex-col md:flex-row md:items-end justify-between mb-12 gap-6">
        <div>
          <div class="inline-flex items-center gap-2 px-3.5 py-1 rounded-full bg-[#EAF3FF] text-[#0056C2] text-xs font-bold uppercase tracking-wider mb-3">
            <Compass class="w-3.5 h-3.5 text-[#0056C2]" />
            <span>Wilayah Utama</span>
          </div>
          <h2 class="text-3xl sm:text-4xl font-extrabold text-[#0B0F19] tracking-tight">
            Wilayah Pengabdian Populer
          </h2>
          <p class="text-base text-[#4B5563] mt-2 max-w-xl">
            Empat dari sembilan kecamatan prioritas lokasi pengabdian mahasiswa Universitas Bina Taruna Gorontalo 2026.
          </p>
        </div>

        <a
          href="#wilayah"
          @click.prevent="router.push('/#wilayah')"
          class="inline-flex items-center gap-2 text-[#0056C2] hover:text-[#003E8F] font-bold text-sm group transition-smooth"
        >
          <span>Jelajahi 9 Kecamatan</span>
          <ArrowUpRight class="w-4 h-4 transition-transform group-hover:translate-x-0.5 group-hover:-translate-y-0.5" />
        </a>
      </div>

      <!-- 4 Cards Grid -->
      <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6">
        <div
          v-for="kec in popularList"
          :key="kec.id"
          @click="handleCardClick(kec)"
          class="group bg-white rounded-2xl border border-[#E5E7EB] overflow-hidden shadow-subtle hover:shadow-card hover:-translate-y-1 transition-all duration-300 cursor-pointer flex flex-col justify-between"
        >
          <!-- Image Container -->
          <div class="relative aspect-[4/3] overflow-hidden bg-[#FAFAFA]">
            <img
              :src="kec.image"
              :alt="kec.name"
              class="w-full h-full object-cover group-hover:scale-103 transition-transform duration-500"
              loading="lazy"
            />
            
            <div class="absolute top-3 right-3 bg-[#0056C2] text-white text-[10px] font-extrabold px-3 py-1 rounded-full uppercase tracking-wider">
              {{ kec.badge }}
            </div>
          </div>

          <!-- Content Below Image -->
          <div class="p-5 flex-1 flex flex-col justify-between">
            <div>
              <h3 class="text-lg font-bold text-[#0B0F19] group-hover:text-[#0056C2] transition-colors">
                Kecamatan {{ kec.name }}
              </h3>
              <div class="flex items-center gap-1.5 text-xs text-[#4B5563] font-semibold mt-1">
                <MapPin class="w-3.5 h-3.5 text-[#0056C2]" />
                <span>{{ kec.city }}, Gorontalo</span>
              </div>
              <p class="text-xs text-[#4B5563] mt-3 leading-relaxed line-clamp-2">
                {{ kec.summary || kec.focus }}
              </p>
            </div>

            <!-- Footer Card Stats -->
            <div class="mt-4 pt-3 border-t border-[#E5E7EB] flex items-center justify-between text-xs">
              <span class="font-bold text-[#0B0F19]">{{ kec.kelurahanCount }} Kelurahan</span>
              <span class="text-[#0056C2] font-bold group-hover:underline flex items-center gap-1">
                Detail Berita <ArrowUpRight class="w-3.5 h-3.5" />
              </span>
            </div>
          </div>
        </div>
      </div>

    </div>
  </section>
</template>
