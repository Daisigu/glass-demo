<script setup lang="ts">
import { VGlass, type VGlassProps } from "@daisigu/vue-liquid-glass";

const model = defineModel<VGlassProps>({
  default: {
    as: "div",
    blur: 2,
    scale: 20,
    baseFrequency: 0.01,
    xChannelSelector: "R",
    yChannelSelector: "G",
    numOctaves: 2,
  },
  required: true,
});
const handleBgFileChange = (file: File | null) => {
  if (!(file instanceof File)) {
    bgFileUrl.value = undefined;
    return;
  }
  if (file.type.startsWith("image/")) {
    bgFileUrl.value = {
      url: URL.createObjectURL(file),
      type: "image",
    };
  } else if (file.type.startsWith("video/")) {
    bgFileUrl.value = {
      url: URL.createObjectURL(file),
      type: "video",
    };
  }
};
const bgFileUrl = defineModel<
  | {
      url: string;
      type: "image" | "video";
    }
  | undefined
>("bgFileUrl", {
  default: undefined,
});
const channelOptions = ["R", "G", "B", "A"];
</script>

<template>
  <VGlass v-bind="model" class="flex flex-col gap-6">
    <UFormField :help="model.blur?.toString()" label="Blur" name="blur">
      <USlider
        class="w-full"
        v-model="model.blur"
        :min="0"
        :max="20"
        :step="0.5"
      />
    </UFormField>

    <UFormField :help="model.scale?.toString()" label="Scale" name="scale">
      <USlider
        class="w-full"
        v-model="model.scale"
        :min="0"
        :max="200"
        :step="1"
      />
    </UFormField>

    <UFormField
      :help="model.baseFrequency?.toString()"
      label="Base Frequency"
      name="baseFrequency"
    >
      <USlider
        class="w-full"
        v-model="model.baseFrequency"
        :min="0"
        :max="0.1"
        :step="0.001"
      />
    </UFormField>

    <UFormField label="X Channel Selector" name="xChannelSelector">
      <USelect
        class="w-full"
        v-model="model.xChannelSelector"
        :items="channelOptions"
      />
    </UFormField>

    <UFormField label="Y Channel Selector" name="yChannelSelector">
      <USelect
        class="w-full"
        v-model="model.yChannelSelector"
        :items="channelOptions"
      />
    </UFormField>

    <UFormField
      :help="model.numOctaves?.toString()"
      label="Number of Octaves"
      name="numOctaves"
    >
      <USlider v-model="model.numOctaves" :min="1" :max="10" :step="1" />
    </UFormField>
    <UButton
      color="primary"
      variant="solid"
      block
      @click="
        model = {
          as: 'div',
          blur: 0,
          scale: 20,
          baseFrequency: 0.01,
          xChannelSelector: 'R',
          yChannelSelector: 'G',
          numOctaves: 2,
        }
      "
    >
      Reset to Default Values
    </UButton>
    <UFormField label="Background image/video" name="bgFileUrl">
      <UFileUpload
        @update:model-value="(file) => handleBgFileChange(file as File | null)"
        label="Drop your image/video here"
        accept="image/*, video/*"
        class="w-full min-h-48"
      />
    </UFormField>
  </VGlass>
</template>
