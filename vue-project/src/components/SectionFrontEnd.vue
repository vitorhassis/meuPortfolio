<script setup>
import { ref } from "vue";

const frontEnd = ["Html", "Css", "JavaScript", "Vue.js", "TailwindCSS"];

const borderColor = ref("rgba(255,255,255,0.2)");

const techBorderColors = {
  Html: ["rgb(255, 138, 76)", "rgb(255, 87, 34)"],
  Css: ["rgb(100, 181, 246)", "rgb(33, 150, 243)"], 
  JavaScript: ["rgb(255, 255, 141)", "rgb(255, 235, 59)"], 
  "Vue.js": ["rgb(129, 199, 132)", "rgb(56, 142, 60)"], 
  TailwindCSS: ["rgb(125, 211, 252)", "rgb(56, 189, 248)"], 
};

let colorInterval = null;

function setBorderColor(tech) {
  const [light, dark] = techBorderColors[tech] || [];
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
    class="flex flex-col rounded-xl p-4 gap-3 transition-all duration-200 ease-in-out text-gray-300 hover:text-white bg-[rgba(163,163,165,0.08)]"
    :style="{ border: '1px solid ' + borderColor }"
  >
    <h1 class="font-medium">FRONTEND</h1>

    <div class="flex flex-wrap gap-2 pb-3">
      <p
        v-for="tech in frontEnd"
        :key="tech"
        class="group relative font-medium px-4 rounded-2xl border border-white/20 hover:border-white/40 hover:bg-white/15 hover:text-white hover:-translate-y-[2px] transition-all duration-200 ease-in-out w-fit cursor-pointer"
        @mouseenter="setBorderColor(tech)"
        @mouseleave="resetBorderColor"
      >
        {{ tech }}
      </p>
    </div>
  </div>
</template>
