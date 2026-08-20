<script setup>
import { ref, computed } from 'vue'
import { useRouter } from 'vue-router'
import { programData } from '../data/program'
import { Leaf, Store, HeartPulse, FileText, Building2, Scale, ArrowUpRight, Sparkles } from 'lucide-vue-next'

const router = useRouter()

const props = defineProps({
  onSelectProgram: Function
})

const activeTab = ref('all')

const categories = [
  { id: 'all', label: 'Semua Program' },
  { id: 'lingkungan', label: 'Lingkungan' },
  { id: 'umkm', label: 'UMKM' },
  { id: 'stunting', label: 'Stunting' },
  { id: 'administrasi', label: 'Administrasi' },
  { id: 'infrastruktur', label: 'Infrastruktur' },
  { id: 'hukum', label: 'Hukum Bisnis' }
]

const iconMap = {
  'p-1': Leaf,
  'p-2': Store,
  'p-3': HeartPulse,
  'p-4': FileText,
  'p-5': Building2,
  'p-6': Scale
}

const filteredPrograms = computed(() => {
  if (activeTab.value === 'all') return programData
  return programData.filter(p => p.category === activeTab.value)
})

const handleCardClick = (prog) => {
  if (props.onSelectProgram) {
    props.onSelectProgram(prog)
  } else if (prog.slug) {
    router.push(`/program/${prog.slug}`)
  }
}
</script>

<template>
  <section id="program" class="py-16 md:py-24 bg-white border-b border-[#E5E7EB]">
    <div class="max-w-[1180px] mx-auto px-5 sm:px-6">
      
      <!-- Section Title -->
      <div class="text-center max-w-3xl mx-auto mb-12">
        <div class="inline-flex items-center gap-2 px-3.5 py-1 rounded-full bg-[#EAF3FF] text-[#0056C2] text-xs font-bold uppercase tracking-wider mb-3">
          <Sparkles class="w-3.5 h-3.5" />
          <span>Fokus Tematik</span>
        </div>
        <h2 class="text-3xl sm:text-4xl lg:text-5xl font-extrabold text-[#0B0F19] tracking-tight mb-4">
          Program Pengabdian Utama
        </h2>
        <p class="text-base sm:text-lg text-[#4B5563]">
          Enam bidang kontribusi lintas disiplin ilmu yang dirancang khusus sesuai sasaran pembangunan berkelanjutan (SDGs).
        </p>
      </div>

      <!-- Filter Tabs -->
      <div class="flex items-center justify-start md:justify-center gap-2 overflow-x-auto pb-4 mb-10 no-scrollbar">
        <button
          v-for="cat in categories"
          :key="cat.id"
          @click="activeTab = cat.id"
          class="px-4 py-2.5 rounded-xl font-bold text-xs sm:text-sm whitespace-nowrap transition-smooth cursor-pointer border"
          :class="[
            activeTab === cat.id
              ? 'bg-[#0056C2] text-white border-[#0056C2] shadow-subtle'
              : 'bg-[#FAFAFA] text-[#4B5563] border-[#E5E7EB] hover:text-[#0B0F19] hover:bg-[#EAF3FF]'
          ]"
        >
          {{ cat.label }}
        </button>
      </div>

      <!-- Cards Grid -->
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6 sm:gap-8">
        <div
          v-for="prog in filteredPrograms"
          :key="prog.id"
          @click="handleCardClick(prog)"
          class="group bg-white rounded-2xl border border-[#E5E7EB] overflow-hidden shadow-subtle hover:shadow-card hover:-translate-y-1 transition-all duration-300 cursor-pointer flex flex-col justify-between"
        >
          <!-- Image Header -->
          <div class="relative aspect-[16/10] overflow-hidden bg-[#FAFAFA]">
            <img
              :src="prog.image"
              :alt="prog.title"
              class="w-full h-full object-cover group-hover:scale-103 transition-transform duration-500"
              loading="lazy"
            />
            <!-- Badges -->
            <div class="absolute top-3 left-3 bg-white text-[#0056C2] text-xs font-bold px-3 py-1 rounded-lg border border-[#E5E7EB] shadow-subtle">
              {{ prog.sdgs }}
            </div>
            
            <div class="absolute top-3 right-3 w-9 h-9 rounded-xl bg-[#0056C2] text-white flex items-center justify-center shadow-subtle">
              <component :is="iconMap[prog.id] || Leaf" class="w-5 h-5" />
            </div>
          </div>

          <!-- Body Content -->
          <div class="p-6 flex-1 flex flex-col justify-between">
            <div>
              <span class="text-xs font-bold text-[#0056C2] uppercase tracking-wider block mb-1">
                {{ prog.categoryLabel }}
              </span>
              <h3 class="text-xl font-bold text-[#0B0F19] group-hover:text-[#0056C2] transition-colors leading-snug mb-2">
                {{ prog.title }}
              </h3>
              <p class="text-xs sm:text-sm text-[#4B5563] leading-relaxed line-clamp-3">
                {{ prog.summary }}
              </p>
            </div>

            <div class="mt-6 pt-4 border-t border-[#E5E7EB] flex items-center justify-between">
              <span class="text-xs font-semibold text-[#0B0F19]">Baca Artikel Berita</span>
              <span class="text-xs font-bold text-[#0056C2] flex items-center gap-1 group-hover:translate-x-1 transition-transform">
                Detail <ArrowUpRight class="w-4 h-4" />
              </span>
            </div>
          </div>

        </div>
      </div>

    </div>
  </section>
</template>
