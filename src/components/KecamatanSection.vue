<script setup>
import { useRouter } from 'vue-router'
import { wilayahData } from '../data/wilayah'
import { MapPin, ArrowUpRight, Navigation } from 'lucide-vue-next'

const router = useRouter()

const props = defineProps({
  onSelectKecamatan: Function
})

const handleCardClick = (kec) => {
  if (props.onSelectKecamatan) {
    props.onSelectKecamatan(kec)
  } else if (kec.slug) {
    router.push(`/wilayah/${kec.slug}`)
  }
}
</script>

<template>
  <section id="wilayah" class="py-16 md:py-24 bg-white border-b border-[#E5E7EB]">
    <div class="max-w-[1180px] mx-auto px-5 sm:px-6">
      
      <!-- Section Header -->
      <div class="text-center max-w-3xl mx-auto mb-12">
        <div class="inline-flex items-center gap-2 px-3.5 py-1 rounded-full bg-[#EAF3FF] text-[#0056C2] text-xs font-bold uppercase tracking-wider mb-3">
          <Navigation class="w-3.5 h-3.5" />
          <span>Sebaran Pengabdian</span>
        </div>
        <h2 class="text-3xl sm:text-4xl lg:text-5xl font-extrabold text-[#0B0F19] tracking-tight mb-4">
          9 Kecamatan Kota Gorontalo
        </h2>
        <p class="text-base sm:text-lg text-[#4B5563]">
          Seluruh wilayah Kota Gorontalo menjadi lokasi pengabdian mahasiswa Universitas Bina Taruna Gorontalo. Klik kartu untuk membaca liputan lengkap tiap kecamatan.
        </p>
      </div>

      <!-- 3x3 Grid for Desktop -->
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
        <div
          v-for="(kec, idx) in wilayahData"
          :key="kec.id"
          @click="handleCardClick(kec)"
          class="group bg-white rounded-2xl p-6 border border-[#E5E7EB] shadow-subtle hover:shadow-card hover:-translate-y-1 transition-all duration-300 cursor-pointer flex flex-col justify-between"
        >
          <div>
            <div class="flex items-center justify-between mb-4">
              <span class="text-2xl font-black text-[#0056C2]">
                0{{ idx + 1 }}
              </span>
              <span class="inline-flex items-center gap-1 text-xs font-bold text-[#0056C2] bg-[#EAF3FF] px-2.5 py-1 rounded-full">
                <MapPin class="w-3.5 h-3.5" />
                <span>{{ kec.kelurahanCount }} Kelurahan</span>
              </span>
            </div>

            <h3 class="text-xl font-bold text-[#0B0F19] group-hover:text-[#0056C2] transition-colors mb-2">
              Kecamatan {{ kec.name }}
            </h3>

            <p class="text-xs sm:text-sm text-[#4B5563] leading-relaxed line-clamp-2 mb-4">
              {{ kec.focus }}
            </p>
          </div>

          <div class="pt-4 border-t border-[#E5E7EB] flex items-center justify-between text-xs">
            <span class="font-bold text-[#0B0F19]">{{ kec.students }}</span>
            <span class="text-[#0056C2] font-bold group-hover:underline flex items-center gap-1">
              Baca Liputan <ArrowUpRight class="w-3.5 h-3.5" />
            </span>
          </div>
        </div>
      </div>

    </div>
  </section>
</template>
