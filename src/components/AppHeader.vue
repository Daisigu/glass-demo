<template>
  <UHeader :toggle="false" class="bg-transparent border-default">
    <template #title>
      <span class="lg:text-2xl font-bold">vue-liquid-glass demo</span>
    </template>
    <template #right>
      <UButton
        color="neutral"
        variant="soft"
        to="https://www.npmjs.com/package/@daisigu/vue-liquid-glass"
        target="_blank"
        icon="i-mdi-npm"
        aria-label="GitHub"
      />
      <UButton
        color="neutral"
        variant="soft"
        to="https://github.com/Daisigu/vue-liquid-glass"
        target="_blank"
        icon="i-mdi-github"
        aria-label="GitHub"
      />
    </template>
  </UHeader>
</template>
