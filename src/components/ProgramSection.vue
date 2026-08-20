<script setup>
import { ref, computed } from 'vue'
import { Leaf, Store, HeartPulse, FileText, Building2, Scale, ArrowUpRight, Sparkles } from 'lucide-vue-next'

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

const programList = [
  {
    id: 'p-1',
    category: 'lingkungan',
    categoryLabel: 'Lingkungan & Sanitasi',
    sdgs: 'SDGs 6 & 13',
    title: 'Konservasi Lingkungan & Bank Sampah',
    description: 'Edukasi pemilahan sampah household, digitalisasi bank sampah kelurahan, dan perbaikan sanitasi lingkungan pemukiman.',
    icon: Leaf,
    image: '/images/kecamatan.png',
    details: 'Program ini difokuskan pada pengelolaan sampah mandiri di tingkat kelurahan melalui pembentukan unit Bank Sampah, edukasi komposting rumah tangga, serta audit lingkungan untuk pencegahan banjir musiman di kawasan Kota Barat dan Dungingi.'
  },
  {
    id: 'p-2',
    category: 'umkm',
    categoryLabel: 'Pemberdayaan UMKM',
    sdgs: 'SDGs 8 & 9',
    title: 'Digitalisasi & Kemasan Produk UMKM',
    description: 'Pendampingan sertifikasi halal, pembuatan legalitas NIB, pemasaran digital via e-commerce, dan redesain kemasan produk unggulan.',
    icon: Store,
    image: '/images/hero.png',
    details: 'Mahasiswa Fakultas Ekonomi & Bisnis UNBITA membantu pelaku UMKM lokal Gorontalo mendaftarkan NIB, sertifikasi halal BPJPH, memasarkan produk di marketplace digital, serta membuat foto katalog produk profesional.'
  },
  {
    id: 'p-3',
    category: 'stunting',
    categoryLabel: 'Pencegahan Stunting',
    sdgs: 'SDGs 3',
    title: 'Posyandu Digital & Gizi Anak',
    description: 'Pemetaan balita risiko stunting, edukasi gizi seimbang bagi ibu hamil, dan modernisasi pencatatan kesehatan Posyandu berbasis mobile.',
    icon: HeartPulse,
    image: '/images/story.png',
    details: 'Kolaborasi lintas disiplin untuk pendataan digital antropometri balita, sosialisasi pemberian makanan tambahan (PMT) berbahan pangan lokal Gorontalo, dan pendampingan keluarga berisiko stunting.'
  },
  {
    id: 'p-4',
    category: 'administrasi',
    categoryLabel: 'Administrasi Publik',
    sdgs: 'SDGs 16',
    title: 'Transparansi & E-Government Kelurahan',
    description: 'Pengembangan sistem informasi pelayanan kelurahan, penataan arsip digital, dan simplifikasi alur pelayanan publik masyarakat.',
    icon: FileText,
    image: '/images/video_poster.png',
    details: 'Peningkatan kapasitas staf kelurahan dalam pengelolaan portal publik, digitalisasi formulir pelayanan warga, serta survei kepuasan masyarakat (SKM) secara transparan.'
  },
  {
    id: 'p-5',
    category: 'infrastruktur',
    categoryLabel: 'Infrastruktur & Ruang',
    sdgs: 'SDGs 11',
    title: 'Pemetaan Permukiman & Ruang Publik',
    description: 'Pemetaan partisipatif berbasis GIS, perencanaan drainase lingkungan, dan redesain ruang terbuka hijau kelurahan.',
    icon: Building2,
    image: '/images/kecamatan.png',
    details: 'Mahasiswa Teknik Sipil, Arsitektur, dan PWK UNBITA berkolaborasi membuat peta digital tata ruang kelurahan, desain konseptual RTH publik, serta evaluasi teknis kondisi jalan lorong dan saluran drainase.'
  },
  {
    id: 'p-6',
    category: 'hukum',
    categoryLabel: 'Hukum Bisnis',
    sdgs: 'SDGs 8',
    title: 'Edukasi Legalitas & Perlindungan Usaha',
    description: 'Penyuluhan hak kekayaan intelektual (HKI), pembuatan draf perjanjian usaha, dan konsultasi legalitas usaha mikro.',
    icon: Scale,
    image: '/images/hero.png',
    details: 'Memberikan bantuan hukum awam bagi pemilik usaha mikro, pendampingan pendaftaran Merek Dagang HKI ke Kemenkumham, serta sosialisasi kesadaran hukum kontrak bagi komunitas usaha lokal.'
  }
]

const filteredPrograms = computed(() => {
  if (activeTab.value === 'all') return programList
  return programList.filter(p => p.category === activeTab.value)
})
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
          @click="onSelectProgram && onSelectProgram(prog)"
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
              <component :is="prog.icon" class="w-5 h-5" />
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
                {{ prog.description }}
              </p>
            </div>

            <div class="mt-6 pt-4 border-t border-[#E5E7EB] flex items-center justify-between">
              <span class="text-xs font-semibold text-[#0B0F19]">Pelajari Pelaksanaan</span>
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
