<script setup>
import { ref } from "vue";

const idiomas = ["Português - Nativo", "Inglês - Intermediário"];

const borderColor = ref("rgba(255,255,255,0.2)");

let colorInterval = null;

function setBorderColor(idioma) {
  clearInterval(colorInterval);

  if (idioma.includes("Português")) {

    const colors = ["rgb(0, 180, 0)", "rgb(255, 215, 0)"];
    let i = 0;
    borderColor.value = colors[0];

    colorInterval = setInterval(() => {
      i = (i + 1) % colors.length;
      borderColor.value = colors[i];
    }, 1100); 
  } else if (idioma.includes("Inglês")) {

    const colors = ["rgb(0, 82, 180)", "rgb(200, 30, 30)", "rgb(255,255,255)"];
    let i = 0;
    borderColor.value = colors[0];

    colorInterval = setInterval(() => {
      i = (i + 1) % colors.length;
      borderColor.value = colors[i];
    }, 1100);
  }
}

function resetBorderColor() {
  clearInterval(colorInterval);
  borderColor.value = "rgba(255,255,255,0.2)";
}
</script>

<template>
  <div
    class="flex flex-col rounded-xl p-4 gap-3 transition-all duration-700 ease-in-out text-gray-300 hover:text-white bg-[rgba(165,163,163,0.08)]"
    :style="{ border: '1px solid ' + borderColor }"
  >
    <h1 class="font-medium">IDIOMAS</h1>

    <div class="flex flex-wrap gap-2 pb-3">
      <p
        v-for="idioma in idiomas"
        :key="idioma"
        class="group relative font-medium px-4 rounded-2xl border border-white/20 hover:border-white/40 hover:bg-white/15 hover:text-white hover:-translate-y-[2px] transition-all duration-200 ease-in-out w-fit cursor-pointer mb-3"
        @mouseenter="setBorderColor(idioma)"
        @mouseleave="resetBorderColor"
      >
        {{ idioma }}
      </p>
    </div>
  </div>
</template>
