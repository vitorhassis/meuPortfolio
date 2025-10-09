<script setup>
import { ref } from "vue";

const ferramentas = [
  "Git",
  "GitHub",
  "Visual Studio Code",
  "Figma",
  "Postman",
  "Visual Studio",
  "Workbench",
];

const borderColor = ref("rgba(255,255,255,0.2)");

const techBorderColors = {
  Git: ["rgb(255, 111, 97)", "rgb(204, 63, 46)"], 
  GitHub: ["rgb(147, 197, 253)", "rgb(59, 130, 246)"], 
  "Visual Studio Code": ["rgb(91, 163, 255)", "rgb(40, 102, 240)"],
  Figma: ["rgb(255, 105, 180)", "rgb(255, 64, 129)"], 
  Postman: ["rgb(255, 165, 0)", "rgb(230, 120, 0)"], 
  "Visual Studio": ["rgb(170, 130, 255)", "rgb(120, 90, 220)"], 
  Workbench: ["rgb(255, 215, 0)", "rgb(255, 180, 0)"], 
};

let colorInterval = null;

function setBorderColor(ferramenta) {
  const [light, dark] = techBorderColors[ferramenta] || [];
  if (!light || !dark) return;

  let toggle = false;
  clearInterval(colorInterval);


  colorInterval = setInterval(() => {
    borderColor.value = toggle ? light : dark;
    toggle = !toggle;
  }, 200); 
}

function resetBorderColor() {
  clearInterval(colorInterval);
  borderColor.value = "rgba(255,255,255,0.2)";
}
</script>

<template>
  <div
    class="flex flex-col rounded-xl p-4 gap-3 transition-all duration-200 ease-in-out text-gray-300 hover:text-white bg-[rgba(165,163,163,0.08)]"
    :style="{ border: '1px solid ' + borderColor }"
  >
    <h1 class="font-medium">FERRAMENTAS</h1>

    <div class="flex flex-wrap gap-2 pb-3">
      <p
        v-for="f in ferramentas"
        :key="f"
        class="group relative font-medium px-4 rounded-2xl border border-white/20 hover:border-white/40 hover:bg-white/15 hover:text-white hover:-translate-y-[2px] transition-all duration-200 ease-in-out w-fit cursor-pointer mb-3"
        @mouseenter="setBorderColor(f)"
        @mouseleave="resetBorderColor"
      >
        {{ f }}
      </p>
    </div>
  </div>
</template>
