<script setup lang="ts">
import { ref } from "vue";
import AnimatedBackground from "./components/AnimatedBackground.vue";
import AppHeader from "./components/AppHeader.vue";
import PropsPanel from "./components/PropsPanel.vue";
import GlassShowcase from "./components/GlassShowcase.vue";
import type { VGlassProps } from "@daisigu/vue-liquid-glass";

const glassProps = ref<VGlassProps>({
  as: "div",
  blur: 2,
  scale: 100,
  baseFrequency: 0.01,
  xChannelSelector: "R",
  yChannelSelector: "G",
  numOctaves: 2,
});
const bgFileUrl = ref<
  | {
      url: string;
      type: "image" | "video";
    }
  | undefined
>(undefined);
</script>

<template>
  <UApp>
    <div class="relative min-h-screen flex flex-col">
      <AnimatedBackground
        class="absolute inset-0 size-full"
        theme="dark"
        bgColor="#1a1a1a"
      />
      <AppHeader />
      <UContainer class="grow flex flex-col">
        <UPage
          :ui="{
            root: 'grow py-4 lg:gap-0',
            left: 'lg:col-span-4',
            center: 'lg:col-span-6',
          }"
        >
          <template #left>
            <div class="h-full relative border border-default border-r-0">
              <PropsPanel
                v-model:bg-file-url="bgFileUrl"
                class="h-full lg:absolute inset-x-1 inset-y-0 overflow-auto p-4"
                v-model="glassProps"
              />
            </div>
          </template>
          <template #default>
            <div class="h-full relative border border-default">
              <GlassShowcase
                :bg-file-url="bgFileUrl"
                class="lg:absolute inset-0 max-h-125 lg:max-h-none"
                :glass-props="glassProps"
              />
            </div>
          </template>
        </UPage>
      </UContainer>
      <UFooter
        class="border-default border-t"
        :ui="{
          center: 'mt-0',
          container: 'py-2',
          left: 'mt-0',
        }"
      >
        <template #default>
          <UButton
            variant="link"
            label="daisigu"
            to="https://github.com/Daisigu"
            target="_blank"
            icon="i-mdi-github"
          />
          <UButton
            variant="link"
            label="daisigu"
            to="https://daisigu.netlify.app/"
            target="_blank"
            icon="heroicons:code-bracket-16-solid"
          />
        </template>
      </UFooter>
    </div>
  </UApp>
</template>
