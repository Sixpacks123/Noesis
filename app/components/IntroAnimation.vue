<script setup lang="ts">
import { ref, onMounted, nextTick } from 'vue'
import { gsap } from 'gsap'

// Contrôler la visibilité de l'animation d'introduction
const introVisible = ref(true)
const introText = ref(null)

// Vérifier si l'animation a déjà été lancée (en utilisant localStorage)
const hasSeenIntro = localStorage.getItem('hasSeenIntro')

onMounted(() => {
  // Si l'animation a déjà été lancée, on ne fait rien
  if (hasSeenIntro) {
    introVisible.value = false
    return
  }

  // Utilisation de nextTick pour attendre que le DOM soit complètement monté
  nextTick(() => {
    if (!introText.value) {
      console.error('introText est nul au moment du montage.')
      return
    }

    // Appliquer une opacité initiale à 0 et une translation de -50px avant l'animation
    gsap.set(introText.value, { opacity: 0, y: 50 })

    // Animation d'introduction avec GSAP
    gsap.timeline()
      .to(introText.value, {
        opacity: 1,
        y: 0,
        scale: 1.2,
        duration: 1.5,
        ease: 'back.out(1.7)',  // Effet de "rebond" pour un effet plus percutant
      })
      .to(introText.value, {
        opacity: 0,
        scale: 1,
        duration: 0.5,
        delay: 0.5,
        ease: 'power2.inOut',
      })
      .add(() => {
        introVisible.value = false // Masquer l'introduction après l'animation

        // Sauvegarder dans localStorage pour ne plus montrer l'intro
        localStorage.setItem('hasSeenIntro', 'true')
      })
  })
})
</script>

<template>
  <div>
    <!-- Animation d'introduction avec v-if pour masquer après l'animation -->
    <div v-if="introVisible" ref="intro" class="intro-container fixed inset-0 bg-black flex items-center justify-center z-50">
      <h1 ref="introText" class="intro-text text-white font-bold shadow-lg uppercase tracking-widest text-[10vw] sm:text-[12vw] md:text-[14vw] lg:text-[16vw] xl:text-[18vw] 2xl:text-[20vw]">
        NOESISDASTUDIO
      </h1>
    </div>
  </div>
</template>
