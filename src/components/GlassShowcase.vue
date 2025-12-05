<script setup lang="ts">
import { VGlass, type VGlassProps } from "@daisigu/vue-liquid-glass";
import { motion } from "motion-v";
import { useTemplateRef } from "vue";

defineProps<{
  glassProps: VGlassProps;
  bgFileUrl?: {
    url: string;
    type: "image" | "video";
  };
}>();
const containerRef = useTemplateRef<HTMLElement>("containerRef");
</script>

<template>
  <div class="h-full flex flex-col relative">
    <img
      v-if="bgFileUrl?.type === 'image'"
      :src="bgFileUrl.url"
      class="absolute inset-0 size-full object-cover"
    />
    <video
      v-else-if="bgFileUrl?.type === 'video'"
      autoplay
      muted
      loop
      playsinline
      :src="bgFileUrl.url"
      class="absolute inset-0 size-full object-cover"
    />
    <div class="p-4">
      <h2 class="text-2xl font-bold mb-2">VGlass Demo</h2>
      <p class="text-sm text-gray-400">
        Various use cases of the component with current settings
      </p>
    </div>

    <div
      ref="containerRef"
      class="grow overflow-y-auto overflow-x-hidden p-4 flex flex-col gap-4 lg:gap-8"
    >
      <!-- Draggable glass element -->
      <motion.div drag :drag-constraints="containerRef ?? false" class="relative z-20">
        <VGlass
          v-bind="glassProps"
          class="p-6 rounded-lg border border-white/20"
        >
          <div class="space-y-4">
            <h4 class="text-xl font-bold text-center">Drag me</h4>
          </div>
        </VGlass>
      </motion.div>
      <!-- Card -->
      <div class="space-y-2">
        <h3 class="text-lg font-semibold">Card</h3>
        <VGlass
          v-bind="glassProps"
          class="p-6 rounded-lg border border-white/20"
        >
          <div class="space-y-4">
            <h4 class="text-xl font-bold">Card Title</h4>
            <p class="text-gray-300">
              This is an example card with liquid glass effect. The text inside
              the card demonstrates how the component works with content.
            </p>
            <div class="flex items-center gap-4">
              <VGlass
                v-bind="glassProps"
                as="button"
                class="px-6 py-2 rounded-lg border border-white/20 backdrop-blur-sm hover:bg-white/20 transition-colors font-medium"
              >
                First Action
              </VGlass>
              <VGlass
                v-bind="glassProps"
                as="button"
                class="px-6 py-2 rounded-lg bg-purple-500/20 border border-white/20 backdrop-blur-sm hover:bg-white/20 transition-colors font-medium"
              >
                Second Action
              </VGlass>
            </div>
          </div>
        </VGlass>
      </div>

      <!-- Buttons -->
      <div class="space-y-2">
        <h3 class="text-lg font-semibold">Buttons</h3>
        <div class="flex flex-wrap gap-4">
          <VGlass
            v-bind="glassProps"
            as="button"
            class="px-6 py-2 rounded-lg border border-white/20 backdrop-blur-sm hover:bg-white/20 transition-colors font-medium"
          >
            Button 1
          </VGlass>
          <VGlass
            v-bind="glassProps"
            as="button"
            class="px-6 py-2 bg-primary/20 rounded-lg border border-white/20 backdrop-blur-sm hover:bg-white/20 transition-colors font-medium"
          >
            Button 2
          </VGlass>
          <VGlass
            v-bind="glassProps"
            as="button"
            class="px-6 py-2 rounded-lg bg-purple-500/20 border border-white/20 backdrop-blur-sm hover:bg-white/20 transition-colors font-medium"
          >
            Button 3
          </VGlass>
          <VGlass
            v-bind="glassProps"
            as="button"
            class="px-6 py-2 rounded-lg bg-black/20 border border-white/20 backdrop-blur-sm hover:bg-white/20 transition-colors font-medium"
          >
            Button 4
          </VGlass>
          <VGlass
            v-bind="glassProps"
            as="button"
            class="px-6 py-2 rounded-lg bg-white/20 border border-white/20 backdrop-blur-sm hover:bg-white/20 transition-colors font-medium"
          >
            Button 5
          </VGlass>
        </div>
      </div>

      <!-- Notification Panel -->
      <div class="space-y-2">
        <h3 class="text-lg font-semibold">Notification Panel</h3>
        <VGlass
          v-bind="glassProps"
          class="p-4 rounded-lg border border-white/20 backdrop-blur-sm"
        >
          <div class="flex items-start gap-3">
            <div
              class="w-10 h-10 rounded-full bg-blue-500/20 flex items-center justify-center shrink-0"
            >
              <span class="text-blue-400 text-xl">ℹ</span>
            </div>
            <div class="flex-1">
              <h4 class="font-semibold mb-1">Information</h4>
              <p class="text-sm text-gray-300">
                This is an example notification panel with liquid glass effect.
              </p>
            </div>
          </div>
        </VGlass>
      </div>

      <!-- Modal Window -->
      <div class="space-y-2">
        <h3 class="text-lg font-semibold">Modal Window</h3>
        <div class="flex items-center justify-center">
          <VGlass
            v-bind="glassProps"
            class="p-8 rounded-xl border border-white/20 backdrop-blur-sm max-w-md w-full"
          >
            <div class="space-y-4">
              <h4 class="text-2xl font-bold">Modal Window</h4>
              <p class="text-gray-300">
                Example of a modal window with liquid glass effect. This
                demonstrates how the component can be used to create modern
                UI elements.
              </p>
              <div class="flex gap-3 justify-end">
                <UButton color="neutral" variant="ghost"> Cancel </UButton>
                <UButton color="primary" variant="solid"> Confirm </UButton>
              </div>
            </div>
          </VGlass>
        </div>
      </div>

      <!-- Badge/Tag -->
      <div class="space-y-2">
        <h3 class="text-lg font-semibold">Badges and Tags</h3>
        <div class="flex flex-wrap gap-3">
          <VGlass
            v-bind="glassProps"
            class="px-3 py-1 rounded-full border border-white/20 backdrop-blur-sm text-sm font-medium"
          >
            New
          </VGlass>
          <VGlass
            v-bind="glassProps"
            class="px-3 py-1 rounded-full border border-white/20 backdrop-blur-sm text-sm font-medium"
          >
            Popular
          </VGlass>
          <VGlass
            v-bind="glassProps"
            class="px-3 py-1 rounded-full border border-white/20 backdrop-blur-sm text-sm font-medium"
          >
            Recommended
          </VGlass>
        </div>
      </div>
    </div>
  </div>
</template>
