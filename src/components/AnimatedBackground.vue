<script setup lang="ts">
import { ref, onMounted, onUnmounted } from "vue";

const canvasRef = ref<HTMLCanvasElement | null>(null);
let animationId: number | null = null;
let particles: Array<{
  x: number;
  y: number;
  vx: number;
  vy: number;
  size: number;
  opacity: number;
}> = [];

const initCanvas = () => {
  const canvas = canvasRef.value;
  if (!canvas) return;

  const ctx = canvas.getContext("2d");
  if (!ctx) return;

  canvas.width = window.innerWidth;
  canvas.height = window.innerHeight;

  // Create particles
  particles = [];
  for (let i = 0; i < 50; i++) {
    particles.push({
      x: Math.random() * canvas.width,
      y: Math.random() * canvas.height,
      vx: (Math.random() - 0.5) * 0.5,
      vy: (Math.random() - 0.5) * 0.5,
      size: Math.random() * 2 + 1,
      opacity: Math.random() * 0.5 + 0.2,
    });
  }

  const animate = () => {
    if (!canvas || !ctx) return;

    ctx.clearRect(0, 0, canvas.width, canvas.height);

    particles.forEach((particle) => {
      particle.x += particle.vx;
      particle.y += particle.vy;

      if (particle.x < 0 || particle.x > canvas.width) particle.vx *= -1;
      if (particle.y < 0 || particle.y > canvas.height) particle.vy *= -1;

      ctx.beginPath();
      ctx.arc(particle.x, particle.y, particle.size, 0, Math.PI * 2);
      ctx.fillStyle =
        `rgba(6, 182, 212, ${particle.opacity})`;
      ctx.fill();
    });

    animationId = requestAnimationFrame(animate);
  };

  animate();
};

const handleResize = () => {
  const canvas = canvasRef.value;
  if (!canvas) return;

  canvas.width = window.innerWidth;
  canvas.height = window.innerHeight;
};
onMounted(() => {
  initCanvas();
  window.addEventListener("resize", handleResize);
});

onUnmounted(() => {
  if (animationId !== null) {
    cancelAnimationFrame(animationId);
  }
  window.removeEventListener("resize", handleResize);
});
</script>

<template>
  <div
    class="fixed inset-0 -z-10 transition-colors duration-500 bg-default"
  >
    <!-- Gradient blobs -->
    <div
      class="absolute top-20 left-10 w-96 h-96 bg-cyan-500/20 rounded-full blur-3xl animate-blob"
    />
    <div
      class="absolute top-40 right-20 w-96 h-96 bg-purple-500/20 rounded-full blur-3xl animate-blob"
      :style="{ animationDelay: '2s' }"
    />
    <div
      class="absolute bottom-20 left-1/3 w-96 h-96 bg-blue-500/20 rounded-full blur-3xl animate-blob"
      :style="{ animationDelay: '4s' }"
    />

    <!-- Particles canvas -->
    <canvas ref="canvasRef" class="absolute inset-0 opacity-60" />

    <!-- Noise texture overlay -->
    <div
      class="absolute inset-0 opacity-10 mix-blend-overlay"
      :style="{
        backgroundImage: `url('data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noiseFilter'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='3' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noiseFilter)'/%3E%3C/svg%3E')`,
      }"
    />
  </div>
</template>
