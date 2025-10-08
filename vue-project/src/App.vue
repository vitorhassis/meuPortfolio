<script setup>
import { onMounted, ref } from "vue";

const frontEnd = ["Html", "Css", "JavaScript", "Vue.js", "TailwindCSS"];
const backEnd = ["C#", ".NET", "ASP.NET", "MySQL"];
const idiomas = ["Português - Nativo", "Inglês - Intermediário"];
const ferramentas = [
  "Git",
  "GitHub",
  "Visual Studio Code",
  "Figma",
  "Postman",
  "Visual Studio",
  "Workbench",
];

const canvasRef = ref(null);

onMounted(() => {
  const canvas = canvasRef.value;
  const ctx = canvas.getContext("2d");

  function resize() {
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;
  }
  resize();
  window.addEventListener("resize", resize);

  // 🌙 carrega lua pixel art
  const moonImg = new Image();
  moonImg.src = "/moon.png"; // coloque o arquivo na pasta public/

  // 🌟 estrelas
  const stars = Array.from({ length: 150 }, () => ({
    x: Math.random() * canvas.width,
    y: Math.random() * canvas.height,
    radius: Math.random() * 1 + 0.1,
    alpha: Math.random(),
    delta: Math.random() * 0.02 + 0.005,
  }));

  // ☄️ cometa
  const comet = {
    x: -100,
    y: Math.random() * (canvas.height * 0.4),
    size: 2,
    speed: 6,
    tail: [],
    visible: true,
    timer: 0,
  };

  function resetComet() {
    comet.x = -100;
    comet.y = Math.random() * (canvas.height * 0.4);
    comet.tail = [];
    comet.visible = true;
    comet.timer = 0;
  }

  function drawComet() {
    if (!comet.visible) return;

    // adiciona ponto na trilha
    comet.tail.unshift({ x: comet.x, y: comet.y });
    if (comet.tail.length > 25) comet.tail.pop();

    // desenha cauda (fade)
    for (let i = 0; i < comet.tail.length; i++) {
      const t = comet.tail[i];
      const alpha = 1 - i / comet.tail.length;
      ctx.fillStyle = `rgba(180,220,255,${alpha * 0.6})`;
      ctx.beginPath();
      ctx.arc(t.x, t.y, comet.size + (i * 0.05), 0, Math.PI * 2);
      ctx.fill();
    }

    // desenha o núcleo
    ctx.fillStyle = "rgba(255,255,255,1)";
    ctx.beginPath();
    ctx.arc(comet.x, comet.y, comet.size + 1.5, 0, Math.PI * 2);
    ctx.fill();

    // movimento diagonal
    comet.x += comet.speed;
    comet.y += comet.speed * 0.25;

    // se saiu da tela, espera um tempo e reseta
    if (comet.x > canvas.width + 100 || comet.y > canvas.height * 0.7) {
      comet.visible = false;
      setTimeout(resetComet, 5000 + Math.random() * 5000); // reaparece entre 5–10s
    }
  }

  function animate() {
    // fundo do céu
    ctx.fillStyle = "#080b16";
    ctx.fillRect(0, 0, canvas.width, canvas.height);

    // --- LUA ---
    if (moonImg.complete) {
      const moonSize = 50;
      const moonX = canvas.width - moonSize - 120;
      const moonY = 80;

      // brilho da lua


      ctx.drawImage(moonImg, moonX, moonY, moonSize, moonSize);
    }

    // --- ESTRELAS ---
    for (const s of stars) {
      s.alpha += s.delta;
      if (s.alpha <= 0 || s.alpha >= 1) s.delta = -s.delta;

      ctx.globalAlpha = s.alpha;
      ctx.fillStyle = "white";
      ctx.beginPath();
      ctx.arc(s.x, s.y, s.radius, 0, Math.PI * 2);
      ctx.fill();

      const grad = ctx.createRadialGradient(s.x, s.y, 0, s.x, s.y, s.radius * 3);
      grad.addColorStop(0, "rgba(255,255,255,0.8)");
      grad.addColorStop(1, "rgba(255,255,255,0)");
      ctx.fillStyle = grad;
      ctx.beginPath();
      ctx.arc(s.x, s.y, s.radius * 3, 0, Math.PI * 2);
      ctx.fill();
    }

    // ☄️ desenha cometa
    drawComet();

    ctx.globalAlpha = 1;
    requestAnimationFrame(animate);
  }

  animate();
});
</script>

<template>
  <main class="relative flex justify-center items-center text-gray-300 overflow-x-hidden overflow-y-auto">
    <!-- 🌠 Fundo de estrelas -->
    <canvas ref="canvasRef" class="fixed inset-0 w-screen h-screen z-0 pointer-events-none block"></canvas>

    <!-- 🧠 Conteúdo -->
    <section
      class="mt-10 mb-10 relative z-10 bg-[rgba(35,30,38,0.26)] min-h-screen flex flex-col p-6 max-w-2xl mx-auto gap-3 border border-white/20 rounded-xl">
      <!-- Navbar -->
      <nav>
        <ul class="flex gap-x-8 font-semibold">
          <li>Vitor Assis</li>
          <li>about</li>
          <li>projects</li>
          <li>content</li>
        </ul>
      </nav>

      <!-- Sobre -->
      <div>
        <h1 class="text-lg font-bold">WHO I AM</h1>
        <p class="text-gray-300">
          Estudante de Engenharia de Software, aprendo por conta própria desde o
          início do curso e gosto de transformar o que estudo em projetos
          práticos.
        </p>
      </div>

      <!-- Faculdade -->
      <div>
        <h1 class="text-lg font-bold">CURRENTLY STUDYING</h1>
        <p class="text-gray-300">
          O curso de Engenharia de Software na Unicesumar proporciona uma
          formação completa em programação, bancos de dados e engenharia de
          requisitos, além de abordar temas como inteligência artificial,
          segurança, estrutura de dados e desenvolvimento mobile — preparando o
          aluno para atuar de forma estratégica em diferentes áreas da
          tecnologia.
        </p>
      </div>

      <!-- FRONTEND -->
      <div
        class="flex flex-col bg-[rgba(163,163,165,0.08)] border border-white/20 rounded-xl p-4 gap-3 hover:border-white/40 transition-all duration-300 ease-in-out text-gray-300 hover:text-white"
      >
        <h1 class="font-medium">FRONTEND</h1>
        <div class="flex flex-wrap gap-2 pb-3">
          <p
            v-for="tech in frontEnd"
            :key="tech"
            class="group relative font-medium px-4 rounded-2xl border border-white/20 hover:border-white/40 hover:bg-white/15 hover:text-white hover:-translate-y-[2px] transition-all duration-300 ease-in-out w-fit text-gray-300"
          >
            {{ tech }}
            <span
              class="absolute bottom-0 left-0 w-full h-[1px] bg-white/80 rounded-b-full scale-x-0 group-hover:scale-x-100 origin-left transition-transform duration-300"
            ></span>
          </p>
        </div>
      </div>

      <!-- BACKEND -->
      <div
        class="flex flex-col bg-[rgba(165,163,163,0.08)] border border-white/20 rounded-xl p-4 gap-3 hover:border-white/40 transition-all duration-300 ease-in-out text-gray-300 hover:text-white"
      >
        <h1 class="font-medium">BACKEND</h1>
        <div class="flex flex-wrap gap-2 pb-3">
          <p
            v-for="tech in backEnd"
            :key="tech"
            class="group relative font-medium px-4 rounded-2xl border border-white/20 hover:border-white/40 hover:bg-white/15 hover:text-white hover:-translate-y-[2px] transition-all duration-300 ease-in-out w-fit text-gray-300"
          >
            {{ tech }}
            <span
              class="absolute bottom-0 left-0 w-full h-[1px] bg-white/80 rounded-b-full scale-x-0 group-hover:scale-x-100 origin-left transition-transform duration-300"
            ></span>
          </p>
        </div>
      </div>

      <!-- FERRAMENTAS -->
      <div
        class="flex flex-col bg-[rgba(165,163,163,0.08)] border border-white/20 rounded-xl p-4 gap-3 hover:border-white/40 transition-all duration-300 ease-in-out text-gray-300 hover:text-white"
      >
        <h1 class="font-medium">FERRAMENTAS</h1>
        <div class="flex flex-wrap gap-2 pb-3">
          <p
            v-for="f in ferramentas"
            :key="f"
            class="group relative font-medium px-4 rounded-2xl border border-white/20 hover:border-white/40 hover:bg-white/15 hover:text-white hover:-translate-y-[2px] transition-all duration-300 ease-in-out w-fit text-gray-300 mb-3"
          >
            {{ f }}
            <span
              class="absolute bottom-0 left-0 w-full h-[1px] bg-white/80 rounded-b-full scale-x-0 group-hover:scale-x-100 origin-left transition-transform duration-300"
            ></span>
          </p>
        </div>
      </div>

      <!-- IDIOMAS -->
      <div
        class="flex flex-col bg-[rgba(165,163,163,0.08)] border border-white/20 rounded-xl p-4 gap-3 hover:border-white/40 transition-all duration-300 ease-in-out text-gray-300 hover:text-white"
      >
        <h1 class="font-medium">IDIOMAS</h1>
        <div class="flex flex-wrap gap-2 pb-3">
          <p
            v-for="idioma in idiomas"
            :key="idioma"
            class="group relative font-medium px-4 rounded-2xl border border-white/20 hover:border-white/40 hover:bg-white/15 hover:text-white hover:-translate-y-[2px] transition-all duration-300 ease-in-out w-fit text-gray-300 mb-3"
          >
            {{ idioma }}
            <span
              class="absolute bottom-[1px] left-[6px] w-[calc(100%-1px)] h-[1px] bg-white/80 scale-x-0 group-hover:scale-x-100 origin-left transition-transform duration-300 rounded-full"
            ></span>
          </p>
        </div>
      </div>
    </section>
  </main>
</template>
