<script setup lang="ts">
import { ref, computed } from 'vue'
import { BuildingOfficeIcon, MapPinIcon, CurrencyEuroIcon, UsersIcon, CalendarIcon, PlusIcon } from '@heroicons/vue/24/outline'
import { companies, type Company, getAllIndustries } from '../data/companies'

const selectedCompany = ref<Company | null>(null)
const searchTerm = ref('')
const selectedIndustry = ref('')

const industries = computed(() => getAllIndustries())

const filteredCompanies = computed(() => {
  return companies.filter(company => {
    const matchesSearch = company.name.toLowerCase().includes(searchTerm.value.toLowerCase()) ||
                         company.description.toLowerCase().includes(searchTerm.value.toLowerCase()) ||
                         company.industry.toLowerCase().includes(searchTerm.value.toLowerCase())
    const matchesIndustry = !selectedIndustry.value || company.industry === selectedIndustry.value
    return matchesSearch && matchesIndustry
  })
})

const clearFilters = () => {
  searchTerm.value = ''
  selectedIndustry.value = ''
}
</script>

<template>
  <div class="min-h-screen">
    <!-- Hero Section -->
    <section class="bg-gradient-to-br from-primary-50 to-primary-100 py-16">
      <div class="mx-auto max-w-6xl px-4">
        <div class="text-center">
          <h1 class="text-3xl sm:text-4xl font-bold text-gray-900 mb-4">
            Firmenkatalog
          </h1>
          <p class="text-lg text-gray-600 max-w-3xl mx-auto">
            Entdecken Sie etablierte Unternehmen und Geschäftsmöglichkeiten in München und Umgebung. 
            Wir vermitteln zwischen Käufern und Verkäufern von Firmen und unterstützen bei Nachfolgeregelungen.
          </p>
        </div>
      </div>
    </section>
    
    <!-- Filters -->
    <section class="py-8 bg-white border-b">
      <div class="mx-auto max-w-6xl px-4">
        <div class="flex flex-col md:flex-row gap-4 items-center">
          <div class="flex-1">
            <input 
              v-model="searchTerm"
              type="text" 
              placeholder="Firmenname, Branche oder Beschreibung suchen..."
              class="w-full p-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-primary-500 focus:border-transparent transition-colors duration-200"
            />
          </div>
          <div class="md:w-64">
            <select 
              v-model="selectedIndustry"
              class="w-full p-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-primary-500 focus:border-transparent transition-colors duration-200"
            >
              <option value="">Alle Branchen</option>
              <option v-for="industry in industries" :key="industry" :value="industry">
                {{ industry }}
              </option>
            </select>
          </div>
          <button 
            v-if="searchTerm || selectedIndustry"
            @click="clearFilters"
            class="btn-secondary whitespace-nowrap"
          >
            Filter zurücksetzen
          </button>
        </div>
        
        <div class="mt-4 text-sm text-gray-600">
          {{ filteredCompanies.length }} von {{ companies.length }} Unternehmen
        </div>
      </div>
    </section>
    
    <!-- Companies Grid -->
    <section class="py-12 bg-gray-50">
      <div class="mx-auto max-w-6xl px-4">
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
          <div 
            v-for="company in filteredCompanies" 
            :key="company.id"
            class="card overflow-hidden group cursor-pointer hover:shadow-xl transition-all duration-300 transform hover:-translate-y-1"
            @click="selectedCompany = company"
          >
            <div class="relative overflow-hidden">
              <img 
                :src="company.image" 
                :alt="company.name"
                class="w-full h-48 object-cover group-hover:scale-105 transition-transform duration-300"
              />
              <div class="absolute top-3 left-3 bg-primary-600 text-white px-3 py-1 rounded-full text-xs font-medium">
                {{ company.industry }}
              </div>
              <div class="absolute top-3 right-3 bg-white/90 backdrop-blur-sm text-gray-700 px-2 py-1 rounded text-xs font-medium">
                {{ company.employees }} MA
              </div>
            </div>
            
            <div class="p-6">
              <h3 class="text-xl font-semibold text-gray-900 mb-2 group-hover:text-primary-600 transition-colors duration-200">
                {{ company.name }}
              </h3>
              
              <p class="text-gray-600 mb-4 text-sm line-clamp-2">{{ company.description }}</p>
              
              <div class="space-y-2 mb-4">
                <div class="flex items-center text-gray-500 text-sm">
                  <MapPinIcon class="w-4 h-4 mr-2 flex-shrink-0" />
                  {{ company.location }}
                </div>
                <div class="flex items-center text-gray-500 text-sm">
                  <CalendarIcon class="w-4 h-4 mr-2 flex-shrink-0" />
                  Gegründet {{ company.founded }}
                </div>
              </div>
              
              <div class="flex justify-between items-center">
                <div class="flex items-center">
                  <CurrencyEuroIcon class="w-5 h-5 text-primary-600 mr-1" />
                  <span class="text-lg font-bold text-primary-600">{{ company.revenue }}</span>
                  <span class="text-sm text-gray-500 ml-1">p.a.</span>
                </div>
                <button class="text-primary-600 hover:text-primary-700 font-medium text-sm flex items-center">
                  Details
                  <svg class="w-4 h-4 ml-1" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
                  </svg>
                </button>
              </div>
            </div>
          </div>
        </div>
        
        <!-- Add Company CTA -->
        <div class="mt-12 text-center">
          <div class="card p-8 max-w-2xl mx-auto bg-gradient-to-br from-primary-50 to-white">
            <PlusIcon class="w-12 h-12 text-primary-600 mx-auto mb-4" />
            <h3 class="text-xl font-semibold text-gray-900 mb-2">
              Ihr Unternehmen im Katalog
            </h3>
            <p class="text-gray-600 mb-6">
              Möchten Sie Ihr Unternehmen verkaufen oder sind auf der Suche nach einem Nachfolger? 
              Wir helfen Ihnen dabei, die richtige Lösung zu finden und vermitteln seriöse Interessenten.
            </p>
            <div class="flex flex-col sm:flex-row gap-3 justify-center">
              <router-link to="/kontakt" class="btn-primary">
                Unternehmen eintragen
              </router-link>
              <router-link to="/dienstleistungen" class="btn-secondary">
                Mehr über Firmenvermittlung
              </router-link>
            </div>
          </div>
        </div>
      </div>
    </section>
    
    <!-- Company Detail Modal -->
    <div 
      v-if="selectedCompany" 
      class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center p-4 z-50"
      @click="selectedCompany = null"
    >
      <div 
        class="bg-white rounded-lg max-w-4xl w-full max-h-[90vh] overflow-y-auto"
        @click.stop
      >
        <div class="relative">
          <img 
            :src="selectedCompany.image" 
            :alt="selectedCompany.name"
            class="w-full h-64 object-cover"
          />
          <button 
            @click="selectedCompany = null"
            class="absolute top-4 right-4 bg-white rounded-full p-2 shadow-lg hover:bg-gray-50 transition-colors duration-200"
          >
            <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
            </svg>
          </button>
          <div class="absolute bottom-4 left-4 bg-white/90 backdrop-blur-sm px-3 py-1 rounded-full">
            <span class="text-sm font-medium text-gray-700">{{ selectedCompany.industry }}</span>
          </div>
        </div>
        
        <div class="p-8">
          <div class="mb-8">
            <h2 class="text-3xl font-bold text-gray-900 mb-2">{{ selectedCompany.name }}</h2>
            <p class="text-lg text-gray-600 mb-4">{{ selectedCompany.description }}</p>
            
            <div class="flex flex-wrap gap-2">
              <span 
                v-for="highlight in selectedCompany.highlights" 
                :key="highlight"
                class="bg-primary-100 text-primary-800 px-3 py-1 rounded-full text-sm"
              >
                {{ highlight }}
              </span>
            </div>
          </div>
          
          <div class="grid grid-cols-1 md:grid-cols-2 gap-8 mb-8">
            <div>
              <h3 class="text-lg font-semibold text-gray-900 mb-4">Unternehmensdaten</h3>
              <div class="space-y-3">
                <div class="flex items-center">
                  <MapPinIcon class="w-5 h-5 text-gray-400 mr-3" />
                  <span class="text-gray-600">{{ selectedCompany.location }}</span>
                </div>
                <div class="flex items-center">
                  <UsersIcon class="w-5 h-5 text-gray-400 mr-3" />
                  <span class="text-gray-600">{{ selectedCompany.employees }} Mitarbeiter</span>
                </div>
                <div class="flex items-center">
                  <CalendarIcon class="w-5 h-5 text-gray-400 mr-3" />
                  <span class="text-gray-600">Gegründet {{ selectedCompany.founded }}</span>
                </div>
                <div class="flex items-center">
                  <CurrencyEuroIcon class="w-5 h-5 text-gray-400 mr-3" />
                  <span class="text-gray-600">{{ selectedCompany.revenue }} Jahresumsatz</span>
                </div>
                <div v-if="selectedCompany.details?.legalForm" class="flex items-center">
                  <BuildingOfficeIcon class="w-5 h-5 text-gray-400 mr-3" />
                  <span class="text-gray-600">{{ selectedCompany.details.legalForm }}</span>
                </div>
              </div>
            </div>
            
            <div>
              <h3 class="text-lg font-semibold text-gray-900 mb-4">Spezialisierungen</h3>
              <ul class="space-y-2 mb-6">
                <li 
                  v-for="specialty in selectedCompany.details?.specialties || []" 
                  :key="specialty"
                  class="flex items-center text-gray-600"
                >
                  <div class="w-2 h-2 bg-primary-500 rounded-full mr-3"></div>
                  {{ specialty }}
                </li>
              </ul>
              
              <div v-if="selectedCompany.details?.certifications?.length">
                <h4 class="font-medium text-gray-900 mb-2">Zertifizierungen</h4>
                <div class="flex flex-wrap gap-2">
                  <span 
                    v-for="cert in selectedCompany.details.certifications" 
                    :key="cert"
                    class="bg-green-100 text-green-800 px-2 py-1 rounded text-xs"
                  >
                    {{ cert }}
                  </span>
                </div>
              </div>
            </div>
          </div>
          
          <div class="border-t pt-6">
            <div class="grid grid-cols-1 sm:grid-cols-2 gap-4 mb-6">
              <div class="p-4 bg-gray-50 rounded-lg">
                <h4 class="font-medium text-gray-900 mb-1">Telefon</h4>
                <a :href="`tel:${selectedCompany.contact.phone}`" class="text-primary-600 hover:text-primary-700">
                  {{ selectedCompany.contact.phone }}
                </a>
              </div>
              <div class="p-4 bg-gray-50 rounded-lg">
                <h4 class="font-medium text-gray-900 mb-1">E-Mail</h4>
                <a :href="`mailto:${selectedCompany.contact.email}`" class="text-primary-600 hover:text-primary-700">
                  {{ selectedCompany.contact.email }}
                </a>
              </div>
            </div>
            
            <div class="flex flex-col sm:flex-row gap-4">
              <router-link to="/kontakt" class="btn-primary flex-1 text-center">
                Interesse bekunden
              </router-link>
              <button class="btn-secondary">
                Weitere Informationen anfordern
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.line-clamp-2 {
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}
</style>