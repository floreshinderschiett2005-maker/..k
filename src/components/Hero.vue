<script setup lang="ts">
import { ArrowRightIcon } from '@heroicons/vue/24/outline'
</script>

<template>
  <section id="home" class="relative bg-gradient-to-br from-primary-50 to-primary-100 overflow-hidden">
    <div class="absolute inset-0 bg-white/20"></div>
    <div class="relative mx-auto max-w-6xl px-4 py-16">
      <div class="grid grid-cols-1 lg:grid-cols-2 gap-8 items-center">
        <div class="text-center lg:text-left">
          <h1 class="text-3xl sm:text-4xl lg:text-5xl font-bold text-gray-900 leading-tight">
            Ihr Partner für
            <span class="text-primary-600 block">Immobilien</span>
          </h1>
          <p class="mt-4 text-lg text-gray-600 leading-relaxed">
            Professionelle Immobilienvermittlung mit umfassendem Service. 
            Von der Bewertung bis zum Notarvertrag - wir begleiten Sie durch den gesamten Prozess.
          </p>
          <div class="mt-6 flex flex-col sm:flex-row gap-3 justify-center lg:justify-start">
            <router-link to="/dienstleistungen" class="btn-primary inline-flex items-center">
              Unsere Services
              <ArrowRightIcon class="ml-2 h-4 w-4" />
            </router-link>
            <router-link to="/katalog" class="btn-secondary">
              Aktuelle Angebote
            </router-link>
          </div>
        </div>
        
        <div class="relative">
          <div class="rounded-xl overflow-hidden shadow-xl">
            <img 
              src="/WhatsApp Image 2025-09-01 at 21.35.38 (1).jpeg" 
              alt="Moderne Immobilie" 
              class="w-full h-64 lg:h-80 object-cover"
            />
          </div>
          <div class="absolute -bottom-4 -left-4 w-16 h-16 bg-primary-600 rounded-full opacity-20"></div>
          <div class="absolute -top-4 -right-4 w-20 h-20 bg-primary-400 rounded-full opacity-10"></div>
        </div>
      </div>
    </div>
  </section>
</template>