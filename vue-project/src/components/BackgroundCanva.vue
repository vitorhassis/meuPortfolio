<template>
  <canvas ref="canvasRef" class="fixed inset-0 w-screen h-screen z-0 pointer-events-none block"></canvas>
</template>

<script setup>
import { onMounted, ref } from "vue";

const canvasRef = ref(null);

onMounted(() => {
  const canvas = canvasRef.value;
  const ctx = canvas.getContext("2d");
  function resize() { canvas.width = innerWidth; canvas.height = innerHeight; }
  resize(); window.addEventListener("resize", resize);
  const moon = new Image(); moon.src = "/moon.png";
  const stars = Array.from({ length: 150 }, () => ({
    x: Math.random() * canvas.width,
    y: Math.random() * canvas.height,
    radius: Math.random() * 1 + 0.1,
    alpha: Math.random(),
    delta: Math.random() * 0.02 + 0.005,
  }));

  const comet = { x: -100, y: Math.random() * (canvas.height * 0.4), size: 2, speed: 6, tail: [], visible: true };

  function drawComet() {
    if (!comet.visible) return;
    comet.tail.unshift({ x: comet.x, y: comet.y });
    if (comet.tail.length > 25) comet.tail.pop();
    for (let i = 0; i < comet.tail.length; i++) {
      const t = comet.tail[i];
      ctx.fillStyle = `rgba(180,220,255,${(1 - i / comet.tail.length) * 0.6})`;
      ctx.beginPath(); ctx.arc(t.x, t.y, comet.size + i * 0.05, 0, Math.PI * 2); ctx.fill();
    }
    ctx.fillStyle = "white";
    ctx.beginPath(); ctx.arc(comet.x, comet.y, comet.size + 1.5, 0, Math.PI * 2); ctx.fill();
    comet.x += comet.speed; comet.y += comet.speed * 0.25;
    if (comet.x > canvas.width + 100 || comet.y > canvas.height * 0.7) {
      comet.visible = false; setTimeout(() => Object.assign(comet, { x: -100, y: Math.random() * (canvas.height * 0.4), tail: [], visible: true }), 5000 + Math.random() * 5000);
    }
  }

  function animate() {
    ctx.fillStyle = "#080b16";
    ctx.fillRect(0, 0, canvas.width, canvas.height);
    if (moon.complete) ctx.drawImage(moon, canvas.width - 170, 80, 50, 50);
    for (const s of stars) {
      s.alpha += s.delta; if (s.alpha <= 0 || s.alpha >= 1) s.delta = -s.delta;
      ctx.globalAlpha = s.alpha; ctx.fillStyle = "white";
      ctx.beginPath(); ctx.arc(s.x, s.y, s.radius, 0, Math.PI * 2); ctx.fill();
    }
    drawComet();
    ctx.globalAlpha = 1;
    requestAnimationFrame(animate);
  }
  animate();
});
</script>
