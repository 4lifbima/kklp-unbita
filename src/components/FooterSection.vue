<script setup>
import { MapPin, Mail, Phone, ArrowRight, Instagram, Facebook, Youtube, Linkedin } from 'lucide-vue-next'

const scrollTo = (href) => {
  const element = document.querySelector(href)
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' })
  }
}
</script>

<template>
  <footer class="bg-white border-t border-[#E5E7EB] pt-16 pb-12">
    <div class="max-w-[1180px] mx-auto px-5 sm:px-6">
      
      <!-- 4 Columns Grid -->
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-10 lg:gap-12 pb-12 border-b border-[#E5E7EB]">
        
        <!-- Column 1: Brand Info -->
        <div>
          <a href="#hero" @click.prevent="scrollTo('#hero')" class="flex items-center gap-3 mb-5">
            <div class="flex items-center justify-center transition-smooth">
              <img src="/images/logo-unbita.png" alt="Logo UNBITA" class="w-10 h-10 object-contain">
            </div>
            <div class="flex flex-col">
              <span class="text-xl font-extrabold tracking-tight text-[#0056C2] leading-none">
                KKLP <span class="text-[#0B0F19]">UNBITA</span>
              </span>
              <span class="text-[8px] font-bold text-[#4B5563] tracking-widest uppercase mt-0.5">
                Universitas Bina Taruna Gorontalo
              </span>
            </div>
          </a>

          <p class="text-xs sm:text-sm text-[#4B5563] leading-relaxed mb-6">
            Portal resmi pelaksanaan Kuliah Kerja Lapangan Produktif (KKLP) Universitas Bina Taruna Gorontalo. 45 hari pengabdian berbasis SDGs di 9 Kecamatan Kota Gorontalo.
          </p>

          <!-- Social Media Icons -->
          <div class="flex items-center gap-3">
            <a href="#" class="w-9 h-9 rounded-xl bg-[#FAFAFA] border border-[#E5E7EB] text-[#4B5563] hover:text-[#0056C2] hover:bg-[#EAF3FF] flex items-center justify-center transition-smooth" aria-label="Instagram">
              <Instagram class="w-4 h-4" />
            </a>
            <a href="#" class="w-9 h-9 rounded-xl bg-[#FAFAFA] border border-[#E5E7EB] text-[#4B5563] hover:text-[#0056C2] hover:bg-[#EAF3FF] flex items-center justify-center transition-smooth" aria-label="Facebook">
              <Facebook class="w-4 h-4" />
            </a>
            <a href="#" class="w-9 h-9 rounded-xl bg-[#FAFAFA] border border-[#E5E7EB] text-[#4B5563] hover:text-[#0056C2] hover:bg-[#EAF3FF] flex items-center justify-center transition-smooth" aria-label="YouTube">
              <Youtube class="w-4 h-4" />
            </a>
            <a href="#" class="w-9 h-9 rounded-xl bg-[#FAFAFA] border border-[#E5E7EB] text-[#4B5563] hover:text-[#0056C2] hover:bg-[#EAF3FF] flex items-center justify-center transition-smooth" aria-label="LinkedIn">
              <Linkedin class="w-4 h-4" />
            </a>
          </div>
        </div>

        <!-- Column 2: Navigasi Cepat -->
        <div>
          <h4 class="text-xs font-extrabold text-[#0B0F19] uppercase tracking-wider mb-4">
            Navigasi Halaman
          </h4>
          <ul class="space-y-3 text-xs sm:text-sm">
            <li>
              <a href="#hero" @click.prevent="scrollTo('#hero')" class="text-[#4B5563] hover:text-[#0056C2] font-medium transition-smooth">
                Beranda Utama
              </a>
            </li>
            <li>
              <a href="#tentang" @click.prevent="scrollTo('#tentang')" class="text-[#4B5563] hover:text-[#0056C2] font-medium transition-smooth">
                Tentang & Esensi KKLP
              </a>
            </li>
            <li>
              <a href="#wilayah" @click.prevent="scrollTo('#wilayah')" class="text-[#4B5563] hover:text-[#0056C2] font-medium transition-smooth">
                Cakupan 9 Kecamatan
              </a>
            </li>
            <li>
              <a href="#program" @click.prevent="scrollTo('#program')" class="text-[#4B5563] hover:text-[#0056C2] font-medium transition-smooth">
                Fokus & Program Utama
              </a>
            </li>
            <li>
              <a href="#kegiatan" @click.prevent="scrollTo('#kegiatan')" class="text-[#4B5563] hover:text-[#0056C2] font-medium transition-smooth">
                Sambutan & Arahan Rektor
              </a>
            </li>
          </ul>
        </div>

        <!-- Column 3: Program Studi & Wilayah -->
        <div>
          <h4 class="text-xs font-extrabold text-[#0B0F19] uppercase tracking-wider mb-4">
            Prodi & Wilayah
          </h4>
          <ul class="space-y-2.5 text-xs sm:text-sm text-[#4B5563]">
            <li>Ilmu Administrasi Publik</li>
            <li>Ilmu Administrasi Bisnis</li>
            <li>Teknik Sipil & Arsitektur</li>
            <li>Perencanaan Wilayah & Kota</li>
            <li>Hukum Bisnis</li>
            <li class="pt-2 font-bold text-[#0B0F19]">Kota Gorontalo (9 Kecamatan)</li>
          </ul>
        </div>

        <!-- Column 4: Kontak & Newsletter Minimalis -->
        <div>
          <h4 class="text-xs font-extrabold text-[#0B0F19] uppercase tracking-wider mb-4">
            Kontak Sekretariat
          </h4>
          
          <ul class="space-y-3 text-xs sm:text-sm text-[#4B5563] mb-6">
            <li class="flex items-start gap-2.5">
              <MapPin class="w-4 h-4 text-[#0056C2] mt-0.5 flex-shrink-0" />
              <span>Jl. Prof. Dr. H. Aloei Saboe, Kota Gorontalo, Indonesia</span>
            </li>
            <li class="flex items-center gap-2.5">
              <Mail class="w-4 h-4 text-[#0056C2] flex-shrink-0" />
              <span>kklp2026@unbita.ac.id</span>
            </li>
            <li class="flex items-center gap-2.5">
              <Phone class="w-4 h-4 text-[#0056C2] flex-shrink-0" />
              <span>+62 (435) 821-2026</span>
            </li>
          </ul>

          <!-- Newsletter minimal -->
          <div>
            <p class="text-xs text-[#4B5563] mb-2 font-medium">Berlangganan Kabar KKLP:</p>
            <form @submit.prevent class="flex gap-2">
              <input
                type="email"
                placeholder="Email Anda..."
                class="w-full px-3 py-2 text-xs bg-[#FAFAFA] border border-[#E5E7EB] rounded-xl text-[#0B0F19] focus:outline-none focus:border-[#0056C2]"
              />
              <button
                type="submit"
                class="px-3 py-2 bg-[#0056C2] text-white rounded-xl hover:bg-[#003E8F] transition-smooth cursor-pointer shadow-subtle"
                aria-label="Kirim"
              >
                <ArrowRight class="w-4 h-4" />
              </button>
            </form>
          </div>

        </div>

      </div>

      <!-- Copyright Bottom Bar -->
      <div class="pt-8 flex flex-col sm:flex-row items-center justify-between gap-4 text-xs text-[#4B5563]">
        <p>© 2026 Kuliah Kerja Lapangan Produktif (KKLP) Universitas Bina Taruna Gorontalo. All rights reserved.</p>
        <div class="flex gap-6 font-medium">
          <a href="#" class="hover:text-[#0056C2] transition-smooth">Privasi</a>
          <a href="#" class="hover:text-[#0056C2] transition-smooth">Syarat & Ketentuan</a>
          <a href="#" class="hover:text-[#0056C2] transition-smooth">Panduan Mahasiswa</a>
        </div>
      </div>

    </div>
  </footer>
</template>
