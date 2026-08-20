<script setup>
import { Clock, MapPin, Calendar, ArrowRight, GraduationCap, Users } from 'lucide-vue-next'

const scrollTo = (href) => {
  const element = document.querySelector(href)
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' })
  }
}
</script>

<template>
  <section id="hero" class="pt-28 pb-16 md:pt-36 md:pb-24 overflow-hidden bg-[#FAFAFA]">
    <div class="max-w-[1180px] mx-auto px-5 sm:px-6">

      <!-- Main Headline & Subheadline -->
      <div class="text-center max-w-3xl mx-auto mb-10 sm:mb-12">
        <h1 class="text-3xl sm:text-5xl md:text-6xl font-extrabold text-[#0B0F19] tracking-tight leading-[1.1] mb-6">
          Bersama Membangun Gorontalo melalui <span class="text-[#0056C2]">KKLP</span>
        </h1>
        <p class="text-base sm:text-lg md:text-xl text-[#4B5563] font-normal leading-relaxed mb-8">
          45 hari pengabdian, 9 kecamatan, dan satu semangat untuk menghadirkan kontribusi nyata berbasis SDGs di Kota Gorontalo.
        </p>

        <!-- Action Buttons -->
        <div class="flex flex-col sm:flex-row items-center justify-center gap-4">
          <a
            href="#program"
            @click.prevent="scrollTo('#program')"
            class="w-full sm:w-auto px-8 py-4 bg-[#0056C2] hover:bg-[#003E8F] text-white font-bold text-base rounded-2xl transition-smooth shadow-card flex items-center justify-center gap-3 cursor-pointer"
          >
            <span>Lihat Program</span>
            <ArrowRight class="w-5 h-5" />
          </a>
          <a
            href="#wilayah"
            @click.prevent="scrollTo('#wilayah')"
            class="w-full sm:w-auto px-8 py-4 bg-white hover:bg-[#EAF3FF] text-[#0B0F19] hover:text-[#0056C2] font-semibold text-base rounded-2xl border border-[#E5E7EB] transition-smooth flex items-center justify-center gap-2 cursor-pointer"
          >
            <MapPin class="w-5 h-5 text-[#0056C2]" />
            <span>Jelajahi Wilayah</span>
          </a>
        </div>
      </div>

      <!-- Hero Visual & Floating Info Bar -->
      <div class="relative max-w-5xl mx-auto mt-4">
        
        <!-- Large Editorial Photo -->
        <div class="relative rounded-3xl overflow-hidden border border-[#E5E7EB] shadow-card bg-white aspect-[16/9] sm:aspect-[21/9]">
          <img
            src="/images/hero.png"
            alt="Mahasiswa Universitas Bina Taruna Gorontalo KKLP"
            class="w-full h-full object-cover object-center transform hover:scale-102 transition-transform duration-700"
            loading="eager"
          />
          
          <!-- Participant Badge -->
          <div class="absolute top-4 right-4 sm:top-6 sm:right-6 bg-white border border-[#E5E7EB] rounded-2xl px-4 py-2.5 shadow-subtle hidden sm:flex items-center gap-3">
            <div class="w-9 h-9 rounded-xl bg-[#EAF3FF] text-[#0056C2] flex items-center justify-center font-bold">
              <Users class="w-5 h-5" />
            </div>
            <div>
              <p class="text-[11px] text-[#4B5563] font-semibold uppercase tracking-wider">Total Peserta</p>
              <p class="text-sm font-extrabold text-[#0B0F19]">1.200+ Mahasiswa</p>
            </div>
          </div>
        </div>

        <!-- Floating Information Bar -->
        <div class="relative sm:-mt-12 mt-6 z-10 px-2 sm:px-6">
          <div class="bg-white rounded-2xl sm:rounded-3xl border border-[#E5E7EB] p-5 sm:p-7 shadow-float grid grid-cols-1 sm:grid-cols-2 md:grid-cols-4 gap-6 items-center">
            
            <!-- Item 1: Durasi -->
            <div class="flex items-center gap-4 sm:border-r border-[#E5E7EB] sm:pr-4">
              <div class="w-12 h-12 rounded-2xl bg-[#EAF3FF] text-[#0056C2] flex items-center justify-center flex-shrink-0">
                <Clock class="w-6 h-6" />
              </div>
              <div>
                <span class="text-[11px] font-bold text-[#4B5563] uppercase tracking-wider block">Durasi</span>
                <span class="text-lg font-extrabold text-[#0B0F19]">45 Hari</span>
                <p class="text-xs text-[#4B5563]">Pengabdian intensif</p>
              </div>
            </div>

            <!-- Item 2: Lokasi -->
            <div class="flex items-center gap-4 md:border-r border-[#E5E7EB] md:pr-4">
              <div class="w-12 h-12 rounded-2xl bg-[#EAF3FF] text-[#0056C2] flex items-center justify-center flex-shrink-0">
                <MapPin class="w-6 h-6" />
              </div>
              <div>
                <span class="text-[11px] font-bold text-[#4B5563] uppercase tracking-wider block">Lokasi</span>
                <span class="text-lg font-extrabold text-[#0B0F19]">9 Kecamatan</span>
                <p class="text-xs text-[#4B5563]">Kota Gorontalo</p>
              </div>
            </div>

            <!-- Item 3: Pelepasan -->
            <div class="flex items-center gap-4 sm:border-r border-[#E5E7EB] sm:pr-4">
              <div class="w-12 h-12 rounded-2xl bg-[#EAF3FF] text-[#0056C2] flex items-center justify-center flex-shrink-0">
                <Calendar class="w-6 h-6" />
              </div>
              <div>
                <span class="text-[11px] font-bold text-[#4B5563] uppercase tracking-wider block">Pelepasan</span>
                <span class="text-lg font-extrabold text-[#0B0F19]">29 Juni 2026</span>
                <p class="text-xs text-[#4B5563]">Seremonial resmi</p>
              </div>
            </div>

            <!-- Item 4: Program Studi -->
            <div class="flex items-center gap-4">
              <div class="w-12 h-12 rounded-2xl bg-[#EAF3FF] text-[#0056C2] flex items-center justify-center flex-shrink-0">
                <GraduationCap class="w-6 h-6" />
              </div>
              <div>
                <span class="text-[11px] font-bold text-[#4B5563] uppercase tracking-wider block">Kolaborasi</span>
                <span class="text-lg font-extrabold text-[#0B0F19]">6 Prodi UNBITA</span>
                <p class="text-xs text-[#4B5563]">Lintas disiplin ilmu</p>
              </div>
            </div>

          </div>
        </div>

      </div>

    </div>
  </section>
</template>
