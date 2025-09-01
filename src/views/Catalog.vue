<script setup lang="ts">
import { ref, computed } from 'vue'
import { BuildingOfficeIcon, MapPinIcon, CurrencyEuroIcon, UsersIcon, CalendarIcon } from '@heroicons/vue/24/outline'

// Company listings data - easily extendable
const companies = ref([
  {
    id: 1,
    name: 'TechStart GmbH',
    industry: 'Software Development',
    location: 'München-Maxvorstadt',
    employees: '25-50',
    founded: '2019',
    revenue: '2.5M',
    image: '/WhatsApp Image 2025-09-01 at 21.28.14.jpeg',
    description: 'Innovative Software-Entwicklung für digitale Lösungen',
    highlights: [
      'Agile Entwicklungsmethoden',
      'Cloud-native Architektur',
      'Internationale Kunden',
      'Starkes Wachstum'
    ],
    contact: {
      email: 'info@techstart.de',
      phone: '+49 89 123 456'
    }
  },
  {
    id: 2,
    name: 'Baumeister & Co KG',
    industry: 'Baugewerbe',
    location: 'München-Sendling',
    employees: '100-200',
    founded: '1995',
    revenue: '15M',
    image: '/WhatsApp Image 2025-09-01 at 21.33.23.jpeg',
    description: 'Traditionelles Bauunternehmen mit moderner Ausrichtung',
    highlights: [
      '30 Jahre Erfahrung',
      'Nachhaltige Bauweise',
      'Komplettlösungen',
      'Zertifizierte Qualität'
    ],
    contact: {
      email: 'kontakt@baumeister-co.de',
      phone: '+49 89 234 567'
    }
  },
  {
    id: 3,
    name: 'Green Energy Solutions',
    industry: 'Erneuerbare Energien',
    location: 'München-Schwabing',
    employees: '50-75',
    founded: '2015',
    revenue: '8M',
    image: '/WhatsApp Image 2025-09-01 at 21.35.38.jpeg',
    description: 'Spezialist für nachhaltige Energielösungen',
    highlights: [
      'Photovoltaik-Anlagen',
      'Energieberatung',
      'Smart Grid Technologie',
      'Umweltfreundlich'
    ],
    contact: {
      email: 'info@green-energy.de',
      phone: '+49 89 345 678'
    }
  },
  {
    id: 4,
    name: 'Logistik Pro GmbH',
    industry: 'Logistik & Transport',
    location: 'München-Riem',
    employees: '75-100',
    founded: '2010',
    revenue: '12M',
    image: '/WhatsApp Image 2025-09-01 at 21.35.38 (1).jpeg',
    description: 'Moderne Logistiklösungen für den E-Commerce',
    highlights: [
      'Automatisierte Lager',
      'Same-Day Delivery',
      'Nachhaltige Flotte',
      'Digitale Prozesse'
    ],
    contact: {
      email: 'service@logistik-pro.de',
      phone: '+49 89 456 789'
    }
  },
  {
    id: 5,
    name: 'MedTech Innovations',
    industry: 'Medizintechnik',
    location: 'München-Bogenhausen',
    employees: '30-50',
    founded: '2018',
    revenue: '5M',
    image: '/WhatsApp Image 2025-09-01 at 21.33.23 (1).jpeg',
    description: 'Entwicklung innovativer Medizingeräte',
    highlights: [
      'FDA-zugelassene Produkte',
      'Forschung & Entwicklung',
      'Internationale Märkte',
      'Patentierte Technologien'
    ],
    contact: {
      email: 'info@medtech-innovations.de',
      phone: '+49 89 567 890'
    }
  },
  {
    id: 6,
    name: 'Gastro Excellence',
    industry: 'Gastronomie',
    location: 'München-Altstadt',
    employees: '20-30',
    founded: '2012',
    revenue: '3M',
    image: '/WhatsApp Image 2025-09-01 at 21.35.38 (1) copy.jpeg',
    description: 'Premium Gastronomie-Konzepte',
    highlights: [
      'Mehrere Standorte',
      'Regionale Küche',
      'Nachhaltigkeit',
      'Ausgezeichnete Qualität'
    ],
    contact: {
      email: 'info@gastro-excellence.de',
      phone: '+49 89 678 901'
    }
  }
])

const selectedCompany = ref<typeof companies.value[0] | null>(null)
const searchTerm = ref('')
const selectedIndustry = ref('')

const industries = computed(() => {
  const uniqueIndustries = [...new Set(companies.value.map(c => c.industry))]
  return uniqueIndustries.sort()
})

const filteredCompanies = computed(() => {
  return companies.value.filter(company => {
    const matchesSearch = company.name.toLowerCase().includes(searchTerm.value.toLowerCase()) ||
                         company.description.toLowerCase().includes(searchTerm.value.toLowerCase())
    const matchesIndustry = !selectedIndustry.value || company.industry === selectedIndustry.value
    return matchesSearch && matchesIndustry
  })
})

// Function to add new companies (for easy extension)
const addCompany = (newCompany: typeof companies.value[0]) => {
  companies.value.push({
    ...newCompany,
    id: Math.max(...companies.value.map(c => c.id)) + 1
  })
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
            Wir vermitteln zwischen Käufern und Verkäufern von Firmen und Gewerbeimmobilien.
          </p>
        </div>
      </div>
    </section>
    
    <!-- Filters -->
    <section class="py-8 bg-white border-b">
      <div class="mx-auto max-w-6xl px-4">
        <div class="flex flex-col md:flex-row gap-4">
          <div class="flex-1">
            <input 
              v-model="searchTerm"
              type="text" 
              placeholder="Firmenname oder Beschreibung suchen..."
              class="w-full p-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-primary-500 focus:border-transparent"
            />
          </div>
          <div class="md:w-64">
            <select 
              v-model="selectedIndustry"
              class="w-full p-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-primary-500 focus:border-transparent"
            >
              <option value="">Alle Branchen</option>
              <option v-for="industry in industries" :key="industry" :value="industry">
                {{ industry }}
              </option>
            </select>
          </div>
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
            class="card overflow-hidden group cursor-pointer hover:shadow-xl transition-all duration-300"
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
            </div>
            
            <div class="p-6">
              <h3 class="text-xl font-semibold text-gray-900 mb-2 group-hover:text-primary-600 transition-colors duration-200">
                {{ company.name }}
              </h3>
              
              <p class="text-gray-600 mb-4 text-sm">{{ company.description }}</p>
              
              <div class="space-y-2 mb-4">
                <div class="flex items-center text-gray-500 text-sm">
                  <MapPinIcon class="w-4 h-4 mr-2" />
                  {{ company.location }}
                </div>
                <div class="flex items-center text-gray-500 text-sm">
                  <UsersIcon class="w-4 h-4 mr-2" />
                  {{ company.employees }} Mitarbeiter
                </div>
                <div class="flex items-center text-gray-500 text-sm">
                  <CalendarIcon class="w-4 h-4 mr-2" />
                  Gegründet {{ company.founded }}
                </div>
              </div>
              
              <div class="flex justify-between items-center">
                <div class="flex items-center">
                  <CurrencyEuroIcon class="w-5 h-5 text-primary-600 mr-1" />
                  <span class="text-lg font-bold text-primary-600">{{ company.revenue }}</span>
                  <span class="text-sm text-gray-500 ml-1">Umsatz</span>
                </div>
                <button class="text-primary-600 hover:text-primary-700 font-medium text-sm">
                  Details →
                </button>
              </div>
            </div>
          </div>
        </div>
        
        <!-- Add Company CTA -->
        <div class="mt-12 text-center">
          <div class="card p-8 max-w-2xl mx-auto">
            <BuildingOfficeIcon class="w-12 h-12 text-primary-600 mx-auto mb-4" />
            <h3 class="text-xl font-semibold text-gray-900 mb-2">
              Ihr Unternehmen im Katalog
            </h3>
            <p class="text-gray-600 mb-4">
              Möchten Sie Ihr Unternehmen verkaufen oder sind auf der Suche nach einem Nachfolger? 
              Wir helfen Ihnen dabei, die richtige Lösung zu finden.
            </p>
            <router-link to="/kontakt" class="btn-primary">
              Unternehmen eintragen
            </router-link>
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
        </div>
        
        <div class="p-8">
          <div class="mb-6">
            <span class="inline-block bg-primary-100 text-primary-800 px-3 py-1 rounded-full text-sm font-medium mb-3">
              {{ selectedCompany.industry }}
            </span>
            <h2 class="text-3xl font-bold text-gray-900 mb-2">{{ selectedCompany.name }}</h2>
            <p class="text-lg text-gray-600">{{ selectedCompany.description }}</p>
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
              </div>
            </div>
            
            <div>
              <h3 class="text-lg font-semibold text-gray-900 mb-4">Besonderheiten</h3>
              <ul class="space-y-2">
                <li 
                  v-for="highlight in selectedCompany.highlights" 
                  :key="highlight"
                  class="flex items-center text-gray-600"
                >
                  <div class="w-2 h-2 bg-primary-500 rounded-full mr-3"></div>
                  {{ highlight }}
                </li>
              </ul>
            </div>
          </div>
          
          <div class="border-t pt-6">
            <div class="flex flex-col sm:flex-row gap-4">
              <button class="btn-primary flex-1">
                Interesse bekunden
              </button>
              <button class="btn-secondary">
                Weitere Informationen
              </button>
              <a 
                :href="`mailto:${selectedCompany.contact.email}`"
                class="btn-secondary text-center"
              >
                Direktkontakt
              </a>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>