<script setup lang="ts">
import { ref } from 'vue'
import Header from './components/Header.vue'
import Hero from './components/Hero.vue'
import Services from './components/Services.vue'
import Catalog from './components/Catalog.vue'
import About from './components/About.vue'
import Contact from './components/Contact.vue'
import Footer from './components/Footer.vue'

const showCatalogForm = ref(false)
</script>

<template>
  <div class="min-h-screen bg-gray-50">
    <Header />
    <Hero />
    <Services />
    <Catalog :show-form="showCatalogForm" @toggle-form="showCatalogForm = !showCatalogForm" />
    <About />
    <Contact />
    <Footer />
  </div>
</template>