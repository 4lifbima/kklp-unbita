<script setup>
import { Landmark, Briefcase, HardHat, Compass, Map, Scale } from 'lucide-vue-next'

const studyPrograms = [
  {
    name: 'Ilmu Administrasi Publik',
    code: 'IAP',
    icon: Landmark,
    role: 'Tata Kelola Kelurahan & E-Gov'
  },
  {
    name: 'Ilmu Administrasi Bisnis',
    code: 'IAB',
    icon: Briefcase,
    role: 'Pemasaran & Manajemen UMKM'
  },
  {
    name: 'Teknik Sipil',
    code: 'TS',
    icon: HardHat,
    role: 'Audit Infrastruktur & Drainase'
  },
  {
    name: 'Arsitektur',
    code: 'ARS',
    icon: Compass,
    role: 'Desain RTH & Fasilitas Publik'
  },
  {
    name: 'Perencanaan Wilayah & Kota',
    code: 'PWK',
    icon: Map,
    role: 'Pemetaan GIS & Tata Ruang'
  },
  {
    name: 'Hukum Bisnis',
    code: 'HKB',
    icon: Scale,
    role: 'Legalitas Usaha & Hak Cipta'
  }
]
</script>

<template>
  <section class="py-16 bg-[#F8FAFC] border-b border-[#E5E7EB]">
    <div class="max-w-[1180px] mx-auto px-5 sm:px-6">
      
      <div class="flex flex-col md:flex-row md:items-end justify-between mb-8 gap-4">
        <div>
          <span class="text-xs font-bold text-[#0056C2] uppercase tracking-wider block mb-1">
            Lintas Disiplin Ilmu
          </span>
          <h2 class="text-2xl sm:text-3xl font-extrabold text-[#111827]">
            Program Studi Terlibat
          </h2>
        </div>
        <p class="text-sm text-[#6B7280] max-w-md">
          Kolaborasi mahasiswa dari 6 program studi fakultas untuk menghadirkan solusi komprehensif bagi masyarakat Gorontalo.
        </p>
      </div>

      <!-- Horizontal Chips / Grid -->
      <div class="grid grid-cols-2 sm:grid-cols-3 lg:grid-cols-6 gap-4">
        <div
          v-for="prodi in studyPrograms"
          :key="prodi.name"
          class="bg-white rounded-2xl p-4 border border-[#E5E7EB] shadow-soft hover:shadow-card hover:-translate-y-1 transition-all duration-300 flex flex-col justify-between"
        >
          <div class="w-10 h-10 rounded-xl bg-[#EAF3FF] text-[#0056C2] flex items-center justify-center mb-3">
            <component :is="prodi.icon" class="w-5 h-5" />
          </div>
          <div>
            <span class="text-[10px] font-extrabold text-[#0056C2] bg-[#EAF3FF] px-2 py-0.5 rounded-full inline-block mb-1">
              {{ prodi.code }}
            </span>
            <h3 class="text-sm font-bold text-[#111827] leading-snug">
              {{ prodi.name }}
            </h3>
            <p class="text-xs text-[#6B7280] mt-1.5 leading-snug">
              {{ prodi.role }}
            </p>
          </div>
        </div>
      </div>

    </div>
  </section>
</template>
