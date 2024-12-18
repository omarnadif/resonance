<template>
    <div class="min-h-screen bg-[#e5e4db]">
      <!-- Navigation -->
      <nav class="fixed top-0 w-full bg-[#1d1d1d] z-50">
        <div class="max-w-6xl mx-auto px-4 py-4 flex justify-between items-center">
          <NuxtLink to="/" class="text-[#f2f2f2] text-2xl font-['Anton']">Resonance</NuxtLink>
        </div>
      </nav>
  
      <!-- Search Section -->
      <section class="bg-[#1d1d1d] pt-20 pb-8 px-4">
        <div class="max-w-6xl mx-auto text-center">
          <h1 class="text-[#f2f2f2] text-4xl md:text-5xl font-['Anton'] mb-4">
            Découvrez des Talents Uniques
          </h1>
          <p class="text-[#f2f2f2] mb-8 font-['Poppins']">
            Trouvez le collaborateur idéal pour votre prochain projet musical
          </p>
          <div class="flex flex-col md:flex-row gap-4 max-w-2xl mx-auto">
            <input
              v-model="searchQuery"
              type="text"
              placeholder="Recherchez par compétence, instrument, style..."
              class="flex-1 px-4 py-2 rounded font-['Poppins'] bg-[#f2f2f2]"
            />
            <button 
              @click="search"
              class="bg-[#f2f2f2] text-[#1d1d1d] px-6 py-2 rounded font-['Poppins'] font-medium">
              Rechercher
            </button>
          </div>
        </div>
      </section>
  
      <!-- Main Content -->
      <div class="max-w-6xl mx-auto px-4 py-8 flex flex-col md:flex-row gap-8">
        <!-- Filters Sidebar -->
        <aside class="w-full md:w-64 bg-[#f2f2f2] rounded-lg p-6 h-fit">
          <!-- Categories -->
          <div class="mb-6">
            <h3 class="font-['Anton'] text-[#1d1d1d] text-lg mb-4">Catégories</h3>
            <div class="space-y-2 font-['Poppins']">
              <label class="flex items-center gap-2">
                <input type="checkbox" v-model="filters.categories.musician" />
                <span>Musicien</span>
              </label>
              <label class="flex items-center gap-2">
                <input type="checkbox" v-model="filters.categories.singer" />
                <span>Chanteur</span>
              </label>
              <label class="flex items-center gap-2">
                <input type="checkbox" v-model="filters.categories.composer" />
                <span>Compositeur</span>
              </label>
              <label class="flex items-center gap-2">
                <input type="checkbox" v-model="filters.categories.producer" />
                <span>Producteur</span>
              </label>
            </div>
          </div>
  
          <!-- Styles -->
          <div class="mb-6">
            <h3 class="font-['Anton'] text-[#1d1d1d] text-lg mb-4">Style Musical</h3>
            <div class="space-y-2 font-['Poppins']">
              <label class="flex items-center gap-2">
                <input type="checkbox" v-model="filters.styles.rock" />
                <span>Rock</span>
              </label>
              <label class="flex items-center gap-2">
                <input type="checkbox" v-model="filters.styles.jazz" />
                <span>Jazz</span>
              </label>
              <label class="flex items-center gap-2">
                <input type="checkbox" v-model="filters.styles.pop" />
                <span>Pop</span>
              </label>
              <label class="flex items-center gap-2">
                <input type="checkbox" v-model="filters.styles.electronic" />
                <span>Électronique</span>
              </label>
            </div>
          </div>
  
          <!-- Experience -->
          <div>
            <h3 class="font-['Anton'] text-[#1d1d1d] text-lg mb-4">Expérience</h3>
            <div class="space-y-2 font-['Poppins']">
              <label class="flex items-center gap-2">
                <input type="checkbox" v-model="filters.experience.beginner" />
                <span>Débutant</span>
              </label>
              <label class="flex items-center gap-2">
                <input type="checkbox" v-model="filters.experience.intermediate" />
                <span>Intermédiaire</span>
              </label>
              <label class="flex items-center gap-2">
                <input type="checkbox" v-model="filters.experience.expert" />
                <span>Expert</span>
              </label>
            </div>
          </div>
        </aside>
  
        <!-- Profiles Grid -->
        <main class="flex-1 grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
          <NuxtLink 
            v-for="profile in profiles" 
            :key="profile.id"
            :to="`/profile/${profile.id}`"
            class="bg-[#f2f2f2] rounded-lg overflow-hidden transition-transform duration-300 hover:-translate-y-2">
            <div class="w-full h-48 bg-[#1d1d1d]"></div>
            <div class="p-6">
              <h3 class="font-['Anton'] text-xl mb-2">{{ profile.name }}</h3>
              <p class="text-[#1f2020] font-['Poppins'] mb-4">{{ profile.title }}</p>
              <div class="flex flex-wrap gap-2">
                <span v-for="tag in profile.tags" :key="tag"
                      class="bg-[#e5e4db] px-3 py-1 rounded-full text-sm font-['Poppins']">
                  {{ tag }}
                </span>
              </div>
            </div>
          </NuxtLink>
        </main>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue'
  
  const searchQuery = ref('')
  const profiles = ref([
    {
      id: 1,
      name: 'Thomas Laurent',
      title: 'Guitariste & Compositeur',
      tags: ['Rock', 'Blues', '10 ans d\'exp.']
    },
    {
      id: 2,
      name: 'Sarah Martin',
      title: 'Chanteuse Soul',
      tags: ['Soul', 'Jazz', '5 ans d\'exp.']
    },
    {
      id: 3,
      name: 'Marc Dubois',
      title: 'Producteur & Ingénieur Son',
      tags: ['Hip-Hop', 'Electronic', '15 ans d\'exp.']
    },
    {
      id: 4,
      name: 'Julie Richard',
      title: 'Compositrice & Pianiste',
      tags: ['Classique', 'Film', '8 ans d\'exp.']
    }
  ])
  
  const filters = ref({
    categories: {
      musician: false,
      singer: false,
      composer: false,
      producer: false
    },
    styles: {
      rock: false,
      jazz: false,
      pop: false,
      electronic: false
    },
    experience: {
      beginner: false,
      intermediate: false,
      expert: false
    }
  })
  
  const search = () => {
    console.log('Recherche:', searchQuery.value, 'Filtres:', filters.value)
  }
  </script>