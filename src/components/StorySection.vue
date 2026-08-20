<script setup>
import { CheckCircle2, Users, MapPin, Award, ArrowRight } from 'lucide-vue-next'

const storyPoints = [
  {
    number: '01',
    title: 'Terapkan Ilmu Akademis',
    description: 'Mengintegrasikan teori kuliah dari 6 prodi UNBITA dengan solusi nyata berbasis kebutuhan masyarakat.'
  },
  {
    number: '02',
    title: 'Bangun Kepemimpinan & Karakter',
    description: 'Mengasah kepekaan sosial, kerja sama tim, komunikasi publik, dan jiwa kepemimpinan mahasiswa.'
  },
  {
    number: '03',
    title: 'Hadirkan Dampak Nyata Berkelanjutan',
    description: 'Menghasilkan kontribusi terukur berbasis indikator SDGs untuk pemberdayaan ekonomi dan lingkungan.'
  }
]

const scrollTo = (href) => {
  const element = document.querySelector(href)
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' })
  }
}
</script>

<template>
  <section id="tentang" class="py-16 md:py-24 bg-[#FAFAFA]">
    <div class="max-w-[1180px] mx-auto px-5 sm:px-6">
      
      <div class="grid grid-cols-1 lg:grid-cols-12 gap-12 lg:gap-16 items-center">
        
        <!-- Left Column: Editorial Copy & Numbered List -->
        <div class="lg:col-span-6">
          <div class="inline-flex items-center gap-2 px-3.5 py-1 rounded-full bg-[#EAF3FF] text-[#0056C2] text-xs font-bold uppercase tracking-wider mb-4">
            <Award class="w-3.5 h-3.5" />
            <span>Esensi & Tujuan</span>
          </div>

          <h2 class="text-3xl sm:text-4xl lg:text-5xl font-extrabold text-[#0B0F19] tracking-tight leading-tight mb-6">
            Pengabdian Berkelanjutan untuk Gorontalo
          </h2>

          <p class="text-base sm:text-lg text-[#4B5563] leading-relaxed mb-8">
            KKLP UNBITA 2026 menjadi momentum mahasiswa Universitas Bina Taruna Gorontalo untuk hadir langsung di tengah masyarakat dan menjadi katalisator perubahan positif.
          </p>

          <!-- 3 Numbered Points -->
          <div class="space-y-6 mb-10">
            <div
              v-for="point in storyPoints"
              :key="point.number"
              class="flex gap-5 group p-4 rounded-2xl bg-white border border-[#E5E7EB] shadow-subtle hover:shadow-card transition-all duration-300"
            >
              <!-- Blue Solid Number Badge -->
              <div class="w-11 h-11 rounded-xl bg-[#0056C2] text-white font-extrabold text-base flex items-center justify-center flex-shrink-0 group-hover:bg-[#003E8F] transition-smooth">
                {{ point.number }}
              </div>

              <div>
                <h3 class="text-base font-bold text-[#0B0F19] mb-1 group-hover:text-[#0056C2] transition-colors">
                  {{ point.title }}
                </h3>
                <p class="text-xs sm:text-sm text-[#4B5563] leading-relaxed">
                  {{ point.description }}
                </p>
              </div>
            </div>
          </div>

          <!-- CTA Button -->
          <div>
            <a
              href="#program"
              @click.prevent="scrollTo('#program')"
              class="inline-flex items-center gap-3 px-7 py-3.5 bg-[#0056C2] hover:bg-[#003E8F] text-white font-bold text-sm rounded-xl transition-smooth shadow-subtle cursor-pointer"
            >
              <span>Jelajahi Program Pengabdian</span>
              <ArrowRight class="w-4 h-4" />
            </a>
          </div>
        </div>

        <!-- Right Column: Visual Portrait & Floating Mini Cards -->
        <div class="lg:col-span-6 relative">
          <div class="relative max-w-md mx-auto lg:max-w-none">
            
            <!-- Main Portrait Image -->
            <div class="relative aspect-[4/5] rounded-[28px] overflow-hidden border border-[#E5E7EB] shadow-card bg-white">
              <img
                src="/images/story.png"
                alt="Aktivitas Mahasiswa KKLP UNBITA"
                class="w-full h-full object-cover object-center transform hover:scale-102 transition-transform duration-700"
                loading="lazy"
              />
            </div>

            <!-- Floating Mini Card 1: Participants -->
            <div class="absolute -top-4 -left-4 sm:-left-6 bg-white rounded-2xl border border-[#E5E7EB] p-4 shadow-float flex items-center gap-3">
              <div class="w-10 h-10 rounded-xl bg-[#EAF3FF] text-[#0056C2] flex items-center justify-center font-bold">
                <Users class="w-5 h-5" />
              </div>
              <div>
                <p class="text-[11px] text-[#4B5563] font-semibold uppercase tracking-wider">Mahasiswa</p>
                <p class="text-sm font-extrabold text-[#0B0F19]">1.200+ Peserta</p>
              </div>
            </div>

            <!-- Floating Mini Card 2: Location -->
            <div class="absolute top-1/2 -right-4 sm:-right-6 -translate-y-1/2 bg-white rounded-2xl border border-[#E5E7EB] p-4 shadow-float flex items-center gap-3">
              <div class="w-10 h-10 rounded-xl bg-[#EAF3FF] text-[#0056C2] flex items-center justify-center">
                <MapPin class="w-5 h-5" />
              </div>
              <div>
                <p class="text-[11px] text-[#4B5563] font-semibold uppercase tracking-wider">Wilayah</p>
                <p class="text-sm font-extrabold text-[#0B0F19]">9 Kecamatan</p>
              </div>
            </div>

            <!-- Floating Mini Card 3: SDGs Impact -->
            <div class="absolute -bottom-4 left-6 sm:left-10 bg-white rounded-2xl border border-[#E5E7EB] p-4 shadow-float flex items-center gap-3">
              <div class="w-10 h-10 rounded-xl bg-[#16A34A]/10 text-[#16A34A] flex items-center justify-center">
                <CheckCircle2 class="w-5 h-5" />
              </div>
              <div>
                <p class="text-[11px] text-[#4B5563] font-semibold uppercase tracking-wider">Pendekatan</p>
                <p class="text-sm font-extrabold text-[#0B0F19]">100% Berbasis SDGs</p>
              </div>
            </div>

          </div>
        </div>

      </div>

    </div>
  </section>
</template>
