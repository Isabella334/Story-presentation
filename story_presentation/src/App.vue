<script setup>
import { onMounted, ref } from "vue"
import divider from "./assets/divider.png"
import titleImage from "./assets/title.png"

const showIntro = ref(true)
const showButton = ref(false)

onMounted(() => {
  setTimeout(() => {
    showButton.value = true
  }, 2000)
})

function enterSite() {
  showIntro.value = false
}

const selectedItem = ref(null)

const items = [

  {
    id: "potion",
    side: "jekyll",
    img: "/items/itemj1.png",
    title: "La Potion",
    content: "La potion symbolise l’expérience scientifique de Jekyll pour séparer le bien et le mal."
  },

  {
    id: "lettre",
    side: "jekyll",
    img: "/items/itemj2.png",
    title: "La Lettre",
    content: "La lettre finale révèle la vérité sur la double identité du docteur Jekyll."
  },

  {
    id: "livre",
    side: "jekyll",
    img: "/items/itemj3.png",
    title: "Le Livre et la Plume",
    content: "Ils représentent la recherche intellectuelle et l’esprit analytique de Jekyll."
  },

  {
    id: "microscope",
    side: "jekyll",
    img: "/items/itemj4.png",
    title: "Le Microscope",
    content: "Le microscope symbolise la rationalité scientifique et l’observation méthodique."
  },

  {
    id: "venin",
    side: "jekyll",
    img: "/items/itemj5.png",
    title: "Le Poison",
    content: "Le poison montre que la science peut devenir dangereuse lorsqu’elle dépasse les limites morales."
  },

  // ===== HYDE =====

  {
    id: "couteau",
    side: "hyde",
    img: "/items/itemh1.png",
    title: "Le Couteau",
    content: "Le couteau représente la violence brutale et incontrôlable de Mr Hyde."
  },

  {
    id: "chapeau",
    side: "hyde",
    img: "/items/itemh2.png",
    title: "Le Chapeau",
    content: "Le chapeau symbolise l’apparence extérieure qui cache une nature monstrueuse."
  },

  {
    id: "masque",
    side: "hyde",
    img: "/items/itemh3.png",
    title: "Le Masque Brisé",
    content: "Le masque brisé représente la fragmentation de l’identité et la domination de Hyde."
  },

  {
    id: "canne",
    side: "hyde",
    img: "/items/itemh4.png",
    title: "La Canne",
    content: "La canne devient une arme lors d’un acte de violence, montrant la brutalité de Hyde."
  },

  {
    id: "anneau",
    side: "hyde",
    img: "/items/itemh5.png",
    title: "L’Anneau",
    content: "L’anneau taché de sang symbolise la corruption morale et la perte d’humanité."
  }
]

function openItem(item) {
  selectedItem.value = item
}

function closeModal() {
  selectedItem.value = null
}
</script>

<template>
  <div class="container">

    <transition name="fade">
      <div v-if="showIntro" class="intro">

        <img :src="titleImage" class="intro-title" />

        <button
          v-if="showButton"
          class="enter-btn"
          @click="enterSite"
        >
          Entrer
        </button>

      </div>
    </transition>

    <div v-if="!showIntro">

    <!-- OBJETOS EN EL ESCRITORIO -->
    <div class="desk">
      <img
        v-for="item in items"
        :key="item.id"
        :src="item.img"
        :class="['item', item.id]"
        @click="openItem(item)"
      />
    </div>

    <!-- IMAGEN CENTRAL -->
    <div class="divider">
      <img :src="divider" />
    </div>

    <!-- MODAL -->
    <div v-if="selectedItem" class="modal">
      <div class="modal-content">
        <button class="close" @click="closeModal">×</button>
        <h2>{{ selectedItem.title }}</h2>
        <p>{{ selectedItem.content }}</p>
      </div>
    </div>
    </div>
  </div>
</template>

<style scoped>

.container {
  min-height: 100vh;
  background: linear-gradient(
    to right,
    #fdf7f2 49%,
    #000000 51%
  );
  position: relative;
  overflow: hidden;
}

.desk {
  position: relative;
  width: 100%;
  height: 100vh;
  z-index: 10;
}

.item {
  position: absolute;
  width: 110px;
  cursor: pointer;
  transition: transform 0.3s ease, filter 0.3s ease;
  filter: drop-shadow(6px 10px 12px rgba(0,0,0,0.5));
}

.item:hover {
  transform: scale(1.15) rotate(0deg);
  z-index: 50;
}

/* JEKYLL DISTRIBUCIÓN (más ordenado) */

.potion { top: 20%; left: 15%; transform: rotate(-4deg); }
.lettre { top: 45%; left: 25%; transform: rotate(3deg); }
.livre { top: 65%; left: 10%; transform: rotate(-2deg); }
.microscope { top: 30%; left: 28%; transform: rotate(5deg); }
.venin { top: 70%; left: 30%; transform: rotate(-6deg); }

.couteau { top: 25%; right: 15%; transform: rotate(18deg); }
.chapeau { top: 50%; right: 10%; transform: rotate(-15deg); }
.masque { top: 35%; right: 30%; transform: rotate(-25deg); }
.canne { top: 70%; right: 25%; transform: rotate(22deg); }
.anneau { top: 60%; right: 5%; transform: rotate(30deg); }


.divider {
  position: absolute;
  top: 0;
  left: 50%;
  transform: translateX(-50%);
  height: 100vh;
  display: flex;
  align-items: center;
  z-index: 5;
  pointer-events: none;
}

.divider img {
  height: 100vh;
  mix-blend-mode: multiply;
}

.modal {
  position: fixed;
  inset: 0;
  background: rgba(0,0,0,0.8);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 100;
}

.modal-content {
  background: #f3efe6;
  padding: 40px;
  width: 420px;
  text-align: center;
  position: relative;
  animation: pop 0.25s ease;
}

.close {
  position: absolute;
  right: 15px;
  top: 10px;
  background: none;
  border: none;
  font-size: 1.5rem;
  cursor: pointer;
}

.intro {
  position: fixed;
  inset: 0;
  background: #000000;
  z-index: 200;
}


.intro-title {
  position: absolute;
  top: 40%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 700px;
  opacity: 0;
  animation: fadeIn 1.5s ease forwards;
}

.enter-btn {
  position: absolute;
  top: 70%;
  left: 50%;
  transform: translate(-50%, -50%);
  padding: 14px 45px;
  font-size: 1.1rem;
  letter-spacing: 4px;
  text-transform: uppercase;
  background: transparent;
  border: 1.5px solid #fdf7f2;
  color: #fdf7f2;
  cursor: pointer;
  opacity: 0;
  animation: fadeIn 1.5s ease forwards;
  animation-delay: 1s;
  transition: all 0.4s ease;
}

.enter-btn:hover {
  background: #fdf7f2;
  color: #000;
  letter-spacing: 6px;
  box-shadow: 0 0 25px rgba(255,255,255,0.4);
}


@keyframes fadeIn {
  to { opacity: 1; }
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 1s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

@keyframes pop {
  0% { transform: scale(0.6); }
  100% { transform: scale(1); }
}

</style>
