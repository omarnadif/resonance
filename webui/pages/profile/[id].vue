<template>
    <div v-if="profile" class="min-h-screen bg-[#e5e4db]">
      <!-- Navigation -->
      <nav class="fixed top-0 w-full bg-[#1d1d1d] z-50">
        <div class="max-w-6xl mx-auto px-4 py-4 flex justify-between items-center">
          <NuxtLink to="/" class="text-[#f2f2f2] text-2xl font-['Anton']">Resonance</NuxtLink>
          <button @click="goBack" class="text-[#f2f2f2] font-['Poppins']">Retour</button>
        </div>
      </nav>
  
      <!-- Hero Section -->
      <div class="pt-20">
        <div class="bg-[#1d1d1d] text-[#f2f2f2] py-12">
          <div class="max-w-6xl mx-auto px-4 flex flex-col md:flex-row gap-8 items-center">
            <div class="w-48 h-48 rounded-full overflow-hidden bg-[#1f2020]" />
            
            <div class="flex-1 text-center md:text-left">
              <h1 class="font-['Anton'] text-4xl mb-2">{{ profile.name }}</h1>
              <p class="font-['Poppins'] text-xl mb-4">{{ profile.title }}</p>
              <div class="flex flex-wrap gap-2 justify-center md:justify-start">
                <span v-for="tag in profile.tags" 
                      :key="tag"
                      class="bg-[#e5e4db] text-[#1d1d1d] px-3 py-1 rounded-full text-sm font-['Poppins']">
                  {{ tag }}
                </span>
              </div>
            </div>
  
            <button class="bg-[#f2f2f2] text-[#1d1d1d] px-6 py-3 rounded font-['Poppins'] font-medium hover:bg-[#e5e4db] transition-colors">
              Contacter
            </button>
          </div>
        </div>
      </div>
  
      <!-- Main Content -->
      <main class="max-w-6xl mx-auto px-4 py-8">
        <div class="grid md:grid-cols-3 gap-8">
          <!-- Left Column -->
          <div class="md:col-span-2 space-y-8">
            <section class="bg-[#f2f2f2] rounded-lg p-6">
              <h2 class="font-['Anton'] text-2xl mb-4">À propos</h2>
              <p class="font-['Poppins'] text-[#1f2020] leading-relaxed">
                {{ profile.about }}
              </p>
            </section>
  
            <section v-if="profile.experience?.length" class="bg-[#f2f2f2] rounded-lg p-6">
              <h2 class="font-['Anton'] text-2xl mb-4">Expérience</h2>
              <div class="space-y-4">
                <div v-for="exp in profile.experience" 
                     :key="exp.id" 
                     class="font-['Poppins']">
                  <h3 class="font-semibold">{{ exp.title }}</h3>
                  <p class="text-[#1f2020]">{{ exp.period }}</p>
                  <p class="text-[#1f2020]">{{ exp.description }}</p>
                </div>
              </div>
            </section>
          </div>
  
          <!-- Right Column -->
          <div class="space-y-6">
            <section v-if="profile.skills?.length" class="bg-[#f2f2f2] rounded-lg p-6">
              <h2 class="font-['Anton'] text-2xl mb-4">Compétences</h2>
              <div class="space-y-2">
                <div v-for="skill in profile.skills" 
                     :key="skill.name" 
                     class="font-['Poppins']">
                  <div class="flex justify-between mb-1">
                    <span>{{ skill.name }}</span>
                    <span>{{ skill.level }}/5</span>
                  </div>
                  <div class="h-2 bg-[#e5e4db] rounded">
                    <div class="h-full bg-[#1d1d1d] rounded" 
                         :style="{ width: `${(skill.level / 5) * 100}%` }" />
                  </div>
                </div>
              </div>
            </section>
  
            <section v-if="profile.equipment?.length" class="bg-[#f2f2f2] rounded-lg p-6">
              <h2 class="font-['Anton'] text-2xl mb-4">Équipement</h2>
              <ul class="list-disc list-inside font-['Poppins'] space-y-2">
                <li v-for="item in profile.equipment" 
                    :key="item">
                  {{ item }}
                </li>
              </ul>
            </section>
          </div>
        </div>
      </main>
    </div>
  </template>
  
  <script setup>
  import { ref, onMounted } from 'vue'
  import { useRoute, useRouter } from '#app'
  
  const route = useRoute()
  const router = useRouter()
  const profile = ref(null)
  
  const loadProfile = async () => {
    const profileId = parseInt(route.params.id)
    
    // Données simulées
    profile.value = {
      id: profileId,
      name: 'Thomas Laurent',
      title: 'Guitariste & Compositeur',
      tags: ['Rock', 'Blues', '10 ans d\'exp.'],
      about: 'Passionné de musique depuis mon plus jeune âge, je suis un guitariste polyvalent spécialisé dans le rock et le blues. Avec plus de 10 ans d\'expérience sur scène et en studio, j\'ai collaboré avec de nombreux artistes et groupes.',
      experience: [
        {
          id: 1,
          title: 'Guitariste Lead - The Rockers',
          period: '2018 - Présent',
          description: 'Tournées nationales, enregistrement de 2 albums, composition'
        },
        {
          id: 2,
          title: 'Session Musician - Studio Blue Note',
          period: '2015 - 2018',
          description: 'Enregistrements pour divers artistes, arrangements'
        }
      ],
      skills: [
        { name: 'Guitare électrique', level: 5 },
        { name: 'Composition', level: 4 },
        { name: 'Arrangement', level: 4 },
        { name: 'Production', level: 3 },
        { name: 'Sound Design', level: 3 }
      ],
      equipment: [
        'Gibson Les Paul Custom',
        'Fender Stratocaster American',
        'Mesa Boogie Dual Rectifier',
        'Pédalier Boss GT-1000',
        'Universal Audio Apollo Twin',
        'Pro Tools / Logic Pro X'
      ]
    }
  }
  
  const goBack = () => router.back()
  
  onMounted(() => {
    loadProfile()
  })
  </script>