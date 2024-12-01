<script setup lang="ts">
const links = [
  {
    label: 'Noesis studio',
    children: [
      {
        label:
            'Noesis studio créé par Léa Picot, Webdesigner indépendante qui s\'est ' +
            'lancée dans l\'aventure rennaise en freelance. ' +
            '\n\nSon objectif : vous proposer du technique et du créatif pour vous aider à ' +
            'pleinement réaliser votre projet !'
      }
    ]
  },
  {
    label: 'Nos services',
    children: [
      { label: 'Audit ergonomique', to: '#' },
      { label: 'Consulting UI/UX', to: '#' },
      { label: 'Création de maquette UI/UX', to: '#' },
      { label: 'Création / Refonte de site internet', to: '#' },
      { label: 'Consulting Création d\'identité graphique', to: '#' }
    ]
  }
]
const toast = useToast()

const email = ref('')
const loading = ref(false)

function onSubmit() {
  loading.value = true

  setTimeout(() => {
    toast.add({
      title: 'Subscribed!',
      description: 'You\'ve been subscribed to our newsletter.'
    })

    loading.value = false
  }, 1000)
}
</script>

<template>
  <UFooter>
    <template #top>
      <UFooterColumns :links="links">
        <template #right>
          <div class="space-y-2">
            <h3 class="font-semibold">Travaillons Ensemble !</h3>
            <p>contact@noesisdastudio.com</p>
            <p>06 88 98 65 01</p>
            <UButton
                label="Contactez-nous"
                @click="onSubmit"
                size="sm"
                color="primary"
            />
          </div>
        </template>
      </UFooterColumns>
    </template>

    <template #left>
      <p class="text-gray-500 dark:text-gray-400 text-sm">
        Copyright © {{ new Date().getFullYear() }}. All rights reserved.
      </p>
    </template>

    <template #right>
      <UColorModeButton size="sm" />

      <UButton
        to="https://github.com/nuxt-ui-pro/landing"
        target="_blank"
        icon="i-simple-icons-github"
        aria-label="GitHub"
        color="gray"
        variant="ghost"
      />
    </template>
  </UFooter>
</template>
