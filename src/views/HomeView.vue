<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'
import HeroSection from '../components/HeroSection.vue'
import PopularKecamatan from '../components/PopularKecamatan.vue'
import StorySection from '../components/StorySection.vue'
import ProgramSection from '../components/ProgramSection.vue'
import StudyProgramSection from '../components/StudyProgramSection.vue'
import KecamatanSection from '../components/KecamatanSection.vue'
import VideoSection from '../components/VideoSection.vue'
import DetailModal from '../components/DetailModal.vue'
import { Play, GraduationCap } from 'lucide-vue-next'

const router = useRouter()

const isVideoModalOpen = ref(false)

const handleSelectKecamatan = (kecamatan) => {
  if (kecamatan && kecamatan.slug) {
    router.push(`/wilayah/${kecamatan.slug}`)
  }
}

const handleSelectProgram = (program) => {
  if (program && program.slug) {
    router.push(`/program/${program.slug}`)
  }
}

const openVideoModal = () => {
  isVideoModalOpen.value = true
}
</script>

<template>
  <div>
    <!-- 1. Hero Section -->
    <HeroSection />

    <!-- 2. Popular Kecamatan Section -->
    <PopularKecamatan :onSelectKecamatan="handleSelectKecamatan" />

    <!-- 3. Story Section -->
    <StorySection />

    <!-- 4. Program Section -->
    <ProgramSection :onSelectProgram="handleSelectProgram" />

    <!-- 5. Study Program Section -->
    <StudyProgramSection />

    <!-- 6. Kecamatan Section -->
    <KecamatanSection :onSelectKecamatan="handleSelectKecamatan" />

    <!-- 7. Video Section -->
    <VideoSection :onOpenVideo="openVideoModal" />

    <!-- Video Rektor Modal -->
    <DetailModal
      :isOpen="isVideoModalOpen"
      title="Arahan Rektor UNBITA — KKLP 2026"
      subtitle="Sambutan & Pembekalan Resmi Peserta KKLP"
      @close="isVideoModalOpen = false"
    >
      <div class="space-y-6">
        <div class="relative aspect-[16/9] bg-[#0B0F19] rounded-2xl overflow-hidden flex flex-col items-center justify-center text-white p-6 border border-[#E5E7EB]">
          <div class="w-16 h-16 rounded-full bg-[#0056C2] text-white flex items-center justify-center mb-4 shadow-float">
            <Play class="w-8 h-8 fill-current ml-1" />
          </div>
          <h4 class="text-lg font-bold text-center">Video Arahan Rektor UNBITA</h4>
          <p class="text-xs text-gray-300 mt-1 text-center max-w-md">
            "Mahasiswa hadir di masyarakat bukan sekadar untuk observasi, melainkan untuk memberikan kontribusi nyata berbasis ilmu pengetahuan."
          </p>
          <span class="mt-4 text-[11px] font-mono bg-white/10 px-3 py-1 rounded-full text-gray-200">
            [ Video Embed Official — UNBITA ]
          </span>
        </div>

        <div class="p-4 bg-[#FAFAFA] rounded-2xl border border-[#E5E7EB] space-y-2">
          <div class="flex items-center gap-2 text-xs font-bold text-[#0056C2]">
            <GraduationCap class="w-4 h-4" />
            <span>Poin Utama Sambutan Rektor:</span>
          </div>
          <ul class="text-xs text-[#4B5563] space-y-1.5 list-disc list-inside">
            <li>Menjaga Etika Akademik & Social Sensitivity di Tengah Masyarakat.</li>
            <li>Fokus Pengabdian Berbasis Target SDGs (Zero Hunger, Good Health, Decent Work).</li>
            <li>Sinergi Lintas Disiplin Ilmu untuk Menghasilkan Inovasi Produk.</li>
          </ul>
        </div>
      </div>
    </DetailModal>
  </div>
</template>
