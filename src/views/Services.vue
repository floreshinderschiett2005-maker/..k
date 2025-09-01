<script setup lang="ts">
import { 
  HomeIcon, 
  DocumentTextIcon, 
  CurrencyDollarIcon,
  ShieldCheckIcon,
  PresentationChartLineIcon,
  WrenchScrewdriverIcon,
  BuildingOfficeIcon,
  UserGroupIcon
} from '@heroicons/vue/24/outline'

const services = [
  {
    icon: BuildingOfficeIcon,
    title: 'Gewerbeimmobilien-Vermittlung',
    description: 'Spezialisiert auf die Vermittlung von Bürogebäuden, Produktionsstätten, Lagerhallen und Einzelhandelsflächen für Unternehmen.',
    features: [
      'Standortanalyse für Unternehmen',
      'Gewerbeimmobilien-Portfolio',
      'Mietvertragsverhandlungen',
      'Expansionsberatung'
    ]
  },
  {
    icon: UserGroupIcon,
    title: 'Firmenvermittlung & Nachfolge',
    description: 'Unterstützung bei Firmenübernahmen, Nachfolgeregelungen und strategischen Unternehmenskäufen.',
    features: [
      'Unternehmensbewertung',
      'Nachfolgeplanung',
      'Due Diligence Begleitung',
      'Vertragsverhandlungen'
    ]
  },
  {
    icon: DocumentTextIcon,
    title: 'Verkaufsexposés',
    description: 'Professionelle Verkaufsexposés mit allen wichtigen Daten sind essentiell für erfolgreiche Immobilientransaktionen.',
    features: [
      'Vollständige Objektdokumentation',
      'Professionelle Fotografie',
      'Marktgerechte Präsentation',
      'Digitale und Print-Versionen'
    ]
  },
  {
    icon: CurrencyDollarIcon,
    title: 'Finanzierungsvermittlung',
    description: 'Durch unsere guten Kontakte zu Kreditinstituten finden wir die optimale Finanzierung und öffentliche Förderungen für Sie.',
    features: [
      'Bankenkontakte nutzen',
      'Förderungen identifizieren',
      'Konditionsvergleich',
      'Finanzierungsberatung'
    ]
  },
  {
    icon: ShieldCheckIcon,
    title: 'Versicherungen & Analyse',
    description: 'Immobilien müssen richtig versichert sein. Wir arbeiten mit unabhängigen Maklerbüros für optimalen Schutz.',
    features: [
      'Versicherungsanalyse',
      'Unabhängige Beratung',
      'Schadensabwicklung',
      'Risikobewertung'
    ]
  },
  {
    icon: PresentationChartLineIcon,
    title: 'Nutzungsalternativen',
    description: 'Optimierung nicht optimal nutzbarer Immobilien durch Umbau, Vergrößerung oder Verkleinerung mit Kostenaufstellungen.',
    features: [
      'Nutzungsanalyse',
      'Optimierungsvorschläge',
      'Machbarkeitsstudien',
      'Wirtschaftlichkeitsrechnung'
    ]
  }
]
</script>

<template>
  <div class="min-h-screen">
    <!-- Hero Section -->
    <section class="bg-gradient-to-br from-primary-50 to-primary-100 py-16">
      <div class="mx-auto max-w-6xl px-4">
        <div class="text-center">
          <h1 class="text-3xl sm:text-4xl font-bold text-gray-900 mb-4">
            Unsere Dienstleistungen
          </h1>
          <p class="text-lg text-gray-600 max-w-3xl mx-auto">
            Professionelle Immobilien- und Firmenvermittlung mit umfassendem Service. 
            Von der Bewertung bis zum Notarvertrag begleiten wir Sie durch den gesamten Prozess.
          </p>
        </div>
      </div>
    </section>
    
    <!-- Services Grid -->
    <section class="py-12 bg-white">
      <div class="mx-auto max-w-6xl px-4">
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
          <div 
            v-for="service in services" 
            :key="service.title"
            class="card p-6 group hover:shadow-xl transition-all duration-300"
          >
            <div class="flex items-center mb-4">
              <div class="w-12 h-12 bg-primary-100 rounded-lg flex items-center justify-center group-hover:bg-primary-200 transition-colors duration-200">
                <component :is="service.icon" class="w-6 h-6 text-primary-600" />
              </div>
              <h3 class="ml-3 text-xl font-semibold text-gray-900">{{ service.title }}</h3>
            </div>
            
            <p class="text-gray-600 mb-6 leading-relaxed">{{ service.description }}</p>
            
            <ul class="space-y-2">
              <li 
                v-for="feature in service.features" 
                :key="feature"
                class="flex items-center text-sm text-gray-500"
              >
                <div class="w-2 h-2 bg-primary-500 rounded-full mr-3"></div>
                {{ feature }}
              </li>
            </ul>
          </div>
        </div>
      </div>
    </section>
    
    <!-- CTA Section -->
    <section class="py-12 bg-gray-50">
      <div class="mx-auto max-w-4xl px-4 text-center">
        <h2 class="text-2xl font-bold text-gray-900 mb-4">
          Bereit für Ihr Immobilienprojekt?
        </h2>
        <p class="text-gray-600 mb-6">
          Kontaktieren Sie uns für eine kostenlose Erstberatung
        </p>
        <router-link to="/kontakt" class="btn-primary inline-flex items-center">
          Kostenlose Beratung anfragen
        </router-link>
      </div>
    </section>
  </div>
</template>