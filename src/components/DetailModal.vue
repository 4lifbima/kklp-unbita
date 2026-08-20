<script setup>
import { X } from 'lucide-vue-next'

const props = defineProps({
  isOpen: Boolean,
  title: String,
  subtitle: String
})

const emit = defineEmits(['close'])
</script>

<template>
  <Teleport to="body">
    <div
      v-if="isOpen"
      class="fixed inset-0 z-50 flex items-center justify-center p-4 sm:p-6 overflow-y-auto modal-backdrop transition-opacity duration-300"
      @click.self="emit('close')"
    >
      <div class="relative w-full max-w-2xl bg-white rounded-3xl shadow-float overflow-hidden border border-[#E5E7EB] transition-all transform duration-300">
        <!-- Header -->
        <div class="flex items-center justify-between px-6 py-5 border-b border-[#E5E7EB] bg-[#FAFAFA]">
          <div>
            <h3 class="text-xl font-bold text-[#0B0F19]">{{ title }}</h3>
            <p v-if="subtitle" class="text-xs text-[#4B5563] mt-0.5 font-medium">{{ subtitle }}</p>
          </div>
          <button
            @click="emit('close')"
            class="p-2 rounded-xl text-[#4B5563] hover:text-[#0B0F19] hover:bg-[#E5E7EB] transition-smooth cursor-pointer"
            aria-label="Tutup"
          >
            <X class="w-5 h-5" />
          </button>
        </div>

        <!-- Body -->
        <div class="p-6 sm:p-8 max-h-[75vh] overflow-y-auto">
          <slot></slot>
        </div>

        <!-- Footer -->
        <div class="px-6 py-4 border-t border-[#E5E7EB] bg-[#FAFAFA] flex justify-end">
          <button
            @click="emit('close')"
            class="px-5 py-2.5 bg-[#0056C2] hover:bg-[#003E8F] text-white font-bold text-xs sm:text-sm rounded-xl transition-smooth cursor-pointer shadow-subtle"
          >
            Tutup
          </button>
        </div>
      </div>
    </div>
  </Teleport>
</template>
