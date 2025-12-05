<script setup lang="ts">
import { VGlass } from "@daisigu/vue-liquid-glass";
import AnimatedBackground from "./components/AnimatedBackground.vue";
import AppHeader from "./components/AppHeader.vue";
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
            root: 'grow py-4',
            left: 'lg:col-span-4',
            center: 'lg:col-span-6',
          }"
        >
          <template #left>
            <div class="size-full relative border-default border">
              <div>
                <h2>Hello World</h2>
              </div>
            </div>
          </template>
          <template #default>
            <div
              class="border border-default size-full flex items-center justify-center"
            >
              <VGlass
                :scale="50"
                :blur="2"
                class="size-50 border-2 border-accented animate-[bounce_4s_ease-in-out_infinite]"
              />
            </div>
          </template>
        </UPage>
      </UContainer>
    </div>
  </UApp>
</template>
