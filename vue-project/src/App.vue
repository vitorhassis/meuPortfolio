<script setup>
import backgroundcanva from "@/components/BackgroundCanva.vue";
import navbar from "@/components/Navbar.vue";
import sobre from "@/components/SectionSobre.vue";
import faculdade from "@/components/SectionFaculdade.vue";
import front from "@/components/SectionFrontEnd.vue";
import back from "@/components/SectionBackEnd.vue";
import ferramentas from "@/components/SectionFerramentas.vue";
import idioma from "@/components/SectionIdiomas.vue";
import divisor from "@/components/Div.vue";
import SectionFooter from "@/components/SectionFooter.vue";


</script>

<template >

  <main>
    <backgroundcanva />
    <section class="mt-10 mb-10 relative z-10 bg-[rgba(53,53,53,0.16)] min-h-screen flex flex-col p-9 max-w-lg mx-auto gap-8">
      <navbar class="relative z-10" />
      <divisor />
      <sobre class="relative z-10" />
      <faculdade />
      <front />
      <back />
      <ferramentas />
      <idioma />
      <divisor />
      <SectionFooter />
    </section>
  </main>
</template>
