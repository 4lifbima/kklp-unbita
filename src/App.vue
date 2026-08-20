<script setup>
import Navbar from './components/Navbar.vue'
import FooterSection from './components/FooterSection.vue'
</script>

<template>
  <div class="min-h-screen bg-[#FAFAFA] text-[#0B0F19] flex flex-col font-sans selection:bg-[#EAF3FF] selection:text-[#0056C2]">
    
    <!-- Navigation Bar -->
    <Navbar />

    <!-- Main Content Body (Vue Router View) -->
    <main class="flex-1">
      <router-view />
    </main>

    <!-- Footer -->
    <FooterSection />

  </div>
</template>
