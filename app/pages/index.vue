<script setup lang="ts">
const { data: page } = await useAsyncData('index', () => queryContent('/').findOne())

useSeoMeta({
  title: page.value.title,
  ogTitle: page.value.title,
  description: page.value.description,
  ogDescription: page.value.description
})
</script>

<template>
  <div>
    <!-- Animation d'introduction     <IntroAnimation />
 -->

    <!-- Contenu de la page -->
    <ULandingHero
        :title="page.hero.title"
        :description="page.hero.description"
        :links="page.hero.links"
    >
      <template #headline>
        <UBadge
            v-if="page.hero.headline"
            variant="subtle"
            size="lg"
            class="relative rounded-full font-semibold"
        >
          <NuxtLink
              :to="page.hero.headline.to"
              target="_blank"
              class="focus:outline-none"
              tabindex="-1"
          >
            <span
                class="absolute inset-0"
                aria-hidden="true"
            />
          </NuxtLink>

          {{ page.hero.headline.label }}

          <UIcon
              v-if="page.hero.headline.icon"
              :name="page.hero.headline.icon"
              class="ml-1 w-4 h-4 pointer-events-none"
          />
        </UBadge>
      </template>
    </ULandingHero>

    <ULandingSection
        :title="page.features.title"
        :description="page.features.description"
        :headline="page.features.headline"
    >
      <UPageGrid
        id="features"
        class="scroll-mt-[calc(var(--header-height)+140px+128px+96px)]"
    >
      <UPricingCard
          v-for="(item, index) in page.features.items"
          :key="index"
          v-bind="item"
      />
    </UPageGrid>
    </ULandingSection>
    <ULandingSection
        :title="page.project.title"
        :description="page.project.description"
        :headline="page.project.headline"
    >
      <ULandingGrid
          id="project"
          class="scroll-mt-[calc(var(--header-height)+140px+128px+96px)]"
      >
        <ULandingCard
            v-for="(item, index) in page.project.items"
            :key="index"
            class="col-span-6 row-span-2"
            v-bind="item"
        />
      </ULandingGrid>
    </ULandingSection>
    <ULandingSection class="bg-primary-50 dark:bg-primary-400 dark:bg-opacity-10">
      <ULandingCTA
          v-bind="page.cta"
          :card="false"
      />
    </ULandingSection>
  </div>
</template>
