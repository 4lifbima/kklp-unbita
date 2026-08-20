<script setup>
import { ref } from 'vue'
import Navbar from './components/Navbar.vue'
import HeroSection from './components/HeroSection.vue'
import PopularKecamatan from './components/PopularKecamatan.vue'
import StorySection from './components/StorySection.vue'
import ProgramSection from './components/ProgramSection.vue'
import StudyProgramSection from './components/StudyProgramSection.vue'
import KecamatanSection from './components/KecamatanSection.vue'
import VideoSection from './components/VideoSection.vue'
import FooterSection from './components/FooterSection.vue'
import DetailModal from './components/DetailModal.vue'
import { MapPin, Users, CheckCircle2, Play, Calendar, ShieldCheck, GraduationCap } from 'lucide-vue-next'

// Modals State
const selectedProgram = ref(null)
const isProgramModalOpen = ref(false)

const selectedKecamatan = ref(null)
const isKecamatanModalOpen = ref(false)

const isVideoModalOpen = ref(false)

// Handlers
const openProgramModal = (program) => {
  selectedProgram.value = program
  isProgramModalOpen.value = true
}

const openKecamatanModal = (kecamatan) => {
  selectedKecamatan.value = kecamatan
  isKecamatanModalOpen.value = true
}

const openVideoModal = () => {
  isVideoModalOpen.value = true
}
</script>

<template>
  <div class="min-h-screen bg-[#F8FAFC] text-[#111827] flex flex-col font-sans selection:bg-[#EAF3FF] selection:text-[#0056C2]">
    
    <!-- Navigation Bar -->
    <Navbar />

    <!-- Main Content Body -->
    <main class="flex-1">
      <!-- 1. Hero Section with Floating Search/Stats Card -->
      <HeroSection />

      <!-- 2. Popular Kecamatan Section ("Popular Place" from reference) -->
      <PopularKecamatan :onSelectKecamatan="openKecamatanModal" />

      <!-- 3. Story Section (Esensi & 3 Poin Utama KKLP) -->
      <StorySection />

      <!-- 4. Program Section (Grid 6 Fokus Tematik & Tabs) -->
      <ProgramSection :onSelectProgram="openProgramModal" />

      <!-- 5. Study Program Section (6 Prodi Chips) -->
      <StudyProgramSection />

      <!-- 6. Kecamatan Section (3x3 Sebaran 9 Kecamatan) -->
      <KecamatanSection :onSelectKecamatan="openKecamatanModal" />

      <!-- 7. Video Section (Poster 16:9 + Arahan Rektor) -->
      <VideoSection :onOpenVideo="openVideoModal" />
    </main>

    <!-- Footer -->
    <FooterSection />

    <!-- Program Detail Modal -->
    <DetailModal
      :isOpen="isProgramModalOpen"
      :title="selectedProgram?.title || 'Detail Program'"
      :subtitle="selectedProgram?.categoryLabel ? `Fokus: ${selectedProgram.categoryLabel} (${selectedProgram.sdgs})` : ''"
      @close="isProgramModalOpen = false"
    >
      <div v-if="selectedProgram" class="space-y-6">
        <div class="aspect-[16/9] rounded-2xl overflow-hidden bg-[#F8FAFC] border border-[#E5E7EB]">
          <img :src="selectedProgram.image" :alt="selectedProgram.title" class="w-full h-full object-cover" />
        </div>

        <div>
          <h4 class="text-base font-bold text-[#111827] mb-2">Deskripsi Pelaksanaan</h4>
          <p class="text-sm text-[#6B7280] leading-relaxed">
            {{ selectedProgram.details || selectedProgram.description }}
          </p>
        </div>

        <div class="grid grid-cols-1 sm:grid-cols-2 gap-4 bg-[#F8FAFC] p-4 rounded-2xl border border-[#E5E7EB]">
          <div>
            <span class="text-xs text-[#6B7280] font-medium block">Sasaran SDGs</span>
            <span class="text-sm font-bold text-[#0056C2]">{{ selectedProgram.sdgs }}</span>
          </div>
          <div>
            <span class="text-xs text-[#6B7280] font-medium block">Lokasi Pelaksanaan</span>
            <span class="text-sm font-bold text-[#111827]">9 Kecamatan Kota Gorontalo</span>
          </div>
        </div>
      </div>
    </DetailModal>

    <!-- Kecamatan Detail Modal -->
    <DetailModal
      :isOpen="isKecamatanModalOpen"
      :title="selectedKecamatan ? `Kecamatan ${selectedKecamatan.name}` : 'Detail Kecamatan'"
      subtitle="Kota Gorontalo, Provinsi Gorontalo"
      @close="isKecamatanModalOpen = false"
    >
      <div v-if="selectedKecamatan" class="space-y-6">
        <div class="grid grid-cols-2 gap-4 bg-[#EAF3FF] p-4 rounded-2xl border border-[#0056C2]/20 text-[#0056C2]">
          <div>
            <span class="text-xs font-semibold block uppercase tracking-wider">Jumlah Kelurahan</span>
            <span class="text-xl font-extrabold">{{ selectedKecamatan.kelurahanCount || 7 }} Kelurahan</span>
          </div>
          <div>
            <span class="text-xs font-semibold block uppercase tracking-wider">Alokasi Mahasiswa</span>
            <span class="text-xl font-extrabold">{{ selectedKecamatan.students || '130 Mahasiswa' }}</span>
          </div>
        </div>

        <div>
          <h4 class="text-base font-bold text-[#111827] mb-3 flex items-center gap-2">
            <MapPin class="w-5 h-5 text-[#0056C2]" />
            <span>Daftar Kelurahan Lokasi KKLP</span>
          </h4>
          <div class="flex flex-wrap gap-2">
            <span
              v-for="kel in selectedKecamatan.kelurahanList || ['Kelurahan Pusat', 'Kelurahan Pesisir', 'Kelurahan Timur']"
              :key="kel"
              class="px-3.5 py-1.5 bg-[#F8FAFC] border border-[#E5E7EB] rounded-xl text-xs font-semibold text-[#111827]"
            >
              {{ kel }}
            </span>
          </div>
        </div>

        <div>
          <h4 class="text-base font-bold text-[#111827] mb-2">Fokus Utama Pengabdian</h4>
          <p class="text-sm text-[#6B7280] leading-relaxed bg-[#F8FAFC] p-4 rounded-2xl border border-[#E5E7EB]">
            {{ selectedKecamatan.focus || selectedKecamatan.description }}
          </p>
        </div>
      </div>
    </DetailModal>

    <!-- Video Rektor Modal -->
    <DetailModal
      :isOpen="isVideoModalOpen"
      title="Arahan Rektor UNBITA — KKLP 2026"
      subtitle="Sambutan & Pembekalan Resmi Peserta KKLP"
      @close="isVideoModalOpen = false"
    >
      <div class="space-y-6">
        <div class="relative aspect-[16/9] bg-[#111827] rounded-2xl overflow-hidden flex flex-col items-center justify-center text-white p-6 border border-[#E5E7EB]">
          <div class="w-16 h-16 rounded-full bg-[#0056C2] text-white flex items-center justify-center mb-4 shadow-float">
            <Play class="w-8 h-8 fill-current ml-1" />
          </div>
          <h4 class="text-lg font-bold text-center">Video Arahan Rektor UNBITA</h4>
          <p class="text-xs text-gray-300 mt-1 text-center max-w-md">
            "Mahasiswa hadir di masyarakat bukan sekadar untuk observasi, melainkan untuk memberikan kontribusi nyata berbasis ilmu pengetahuan."
          </p>
          <span class="mt-4 text-[11px] font-mono bg-white/10 px-3 py-1 rounded-full text-gray-200">
            [ Video Embed Ready — UNBITA Official ]
          </span>
        </div>

        <div class="p-4 bg-[#F8FAFC] rounded-2xl border border-[#E5E7EB] space-y-2">
          <div class="flex items-center gap-2 text-xs font-bold text-[#0056C2]">
            <GraduationCap class="w-4 h-4" />
            <span>Poin Utama Sambutan Rektor:</span>
          </div>
          <ul class="text-xs text-[#6B7280] space-y-1.5 list-disc list-inside">
            <li>Pentingnya Menjaga Etika Akademik & Social Sensitivity di Tengah Masyarakat.</li>
            <li>Fokus Pengabdian Berbasis Terget SDGs (Zero Hunger, Good Health, Decent Work).</li>
            <li>Sinergi Antar Mahasiswa Beda Program Studi untuk Menghasilkan Inovasi Produk.</li>
          </ul>
        </div>
      </div>
    </DetailModal>

  </div>
</template>
