<script setup>
import { Play, Video, CheckCircle } from 'lucide-vue-next'

const props = defineProps({
  onOpenVideo: Function
})
</script>

<template>
  <section id="kegiatan" class="py-16 md:py-24 bg-[#FAFAFA]">
    <div class="max-w-[1180px] mx-auto px-5 sm:px-6">
      
      <!-- Section Header -->
      <div class="text-center max-w-3xl mx-auto mb-10">
        <div class="inline-flex items-center gap-2 px-3.5 py-1 rounded-full bg-[#EAF3FF] text-[#0056C2] text-xs font-bold uppercase tracking-wider mb-3">
          <Video class="w-3.5 h-3.5" />
          <span>Sambutan Akademis</span>
        </div>
        <h2 class="text-3xl sm:text-4xl lg:text-5xl font-extrabold text-[#0B0F19] tracking-tight mb-4">
          Arahan Rektor UNBITA
        </h2>
        <p class="text-base sm:text-lg text-[#4B5563]">
          Saksikan pesan mendalam dan visi strategis Rektor Universitas Bina Taruna Gorontalo mengenai esensi pelaksanaan KKLP 2026.
        </p>
      </div>

      <!-- Video Poster Card -->
      <div class="relative max-w-4xl mx-auto rounded-[28px] overflow-hidden border border-[#E5E7EB] shadow-float bg-white aspect-[16/9] group cursor-pointer" @click="onOpenVideo && onOpenVideo()">
        
        <!-- Background Poster Image -->
        <img
          src="/images/video_poster.png"
          alt="Poster Arahan Rektor UNBITA"
          class="w-full h-full object-cover object-center group-hover:scale-103 transition-transform duration-700"
          loading="lazy"
        />

        <!-- Solid Tint Filter for Contrast (No Gradient) -->
        <div class="absolute inset-0 bg-[#0B0F19]/30 transition-opacity group-hover:bg-[#0B0F19]/40"></div>

        <!-- Solid White Circular Play Button in Center -->
        <div class="absolute inset-0 flex flex-col items-center justify-center">
          <div class="w-20 h-20 sm:w-24 sm:h-24 rounded-full bg-white text-[#0056C2] flex items-center justify-center shadow-float group-hover:scale-110 transition-transform duration-300">
            <Play class="w-8 h-8 sm:w-10 sm:h-10 fill-current ml-1" />
          </div>
          
          <div class="mt-4 px-4 py-2 bg-white rounded-xl border border-[#E5E7EB] shadow-subtle flex items-center gap-2">
            <CheckCircle class="w-4 h-4 text-[#0056C2]" />
            <span class="text-xs sm:text-sm font-bold text-[#0B0F19]">
              Putar Video Arahan (03:45)
            </span>
          </div>
        </div>

        <!-- Top Corner Label -->
        <div class="absolute top-4 left-4 sm:top-6 sm:left-6 bg-[#0056C2] text-white text-xs font-bold px-4 py-1.5 rounded-xl uppercase tracking-wider shadow-subtle">
          Pesan Resmi Rektor UNBITA
        </div>

      </div>

    </div>
  </section>
</template>
