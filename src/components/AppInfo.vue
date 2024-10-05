<template>
  <div class="app-info">
    <!-- Versión para pantallas grandes -->
    <div class="d-none d-md-block cardres">
      <div class="mb-3">
        <button class="btn btn-custom btn-icon" @click="toggleCards">
          <i :class="showCards ? 'fas fa-eye-slash' : 'fas fa-eye'"></i>
          {{ showCards ? "Ocultar" : "Mostrar" }}
        </button>
      </div>
      <transition-group
        name="fade"
        tag="div"
        class="d-flex justify-content-between"
      >
        <div
          v-if="showCards"
          v-for="(card, index) in cardsData"
          :key="index"
          class="info-card"
        >
          <h5 :class="card.headerClass">{{ card.title }}</h5>
          <div class="card-content">
            <div class="image-container">
              <img
                v-if="card.logo"
                :src="card.logo"
                :alt="card.title"
                class="logo"
              />
              <img
                v-if="card.image"
                :src="card.image"
                :alt="card.title"
                class="patient-image"
              />
            </div>
            <div class="data-container">
              <p v-for="(item, itemIndex) in card.items" :key="itemIndex">
                <strong>{{ item.label }}:</strong> {{ item.value }}
              </p>
            </div>
          </div>
        </div>
      </transition-group>
    </div>

    <!-- Versión acordeón para pantallas pequeñas -->
    <div class="d-md-none">
      <div class="accordion" id="infoAccordion">
        <div
          v-for="(card, index) in cardsData"
          :key="index"
          class="accordion-item"
        >
          <h2 class="accordion-header" :id="'heading' + index">
            <button
              class="accordion-button"
              type="button"
              data-bs-toggle="collapse"
              :data-bs-target="'#collapse' + index"
              :aria-expanded="index === 0"
              :aria-controls="'collapse' + index"
            >
              {{ card.title }}
            </button>
          </h2>
          <div
            :id="'collapse' + index"
            class="accordion-collapse collapse"
            :class="{ show: index === 0 }"
            :aria-labelledby="'heading' + index"
            data-bs-parent="#infoAccordion"
          >
            <div class="accordion-body">
              <img
                v-if="card.logo"
                :src="card.logo"
                :alt="card.title"
                class="logo"
              />
              <img
                v-if="card.image"
                :src="card.image"
                :alt="card.title"
                class="patient-image"
              />
              <p v-for="(item, itemIndex) in card.items" :key="itemIndex">
                <strong>{{ item.label }}:</strong> {{ item.value }}
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { cardsData } from "../bd/bd.js";

export default {
  name: "AppInfo",
  data() {
    return {
      showCards: true,
      cardsData: cardsData,
    };
  },
  methods: {
    toggleCards() {
      this.showCards = !this.showCards;
    },
  },
};
</script>

<style scoped>
.app-info {
  margin-bottom: 20px;
}

.cardres {
  margin: 20px 115px 20px 115px;
}

.info-card {
  background-color: #ffffff;
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  padding: 20px;
  width: 32%;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  transition: all 0.3s ease;
}

.info-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 6px 12px rgba(0, 0, 0, 0.15);
}

.info-card h5 {
  color: #333;
  background-color: #ffffff !important;
  font-size: 1.2rem;
  margin-bottom: 15px;
  border-bottom: 2px solid #2a3f54;
  padding-bottom: 10px;
}

.card-content {
  display: flex;
}

.image-container {
  flex: 0 0 auto;
  margin-right: 15px;
}

.data-container {
  flex: 1;
}

.logo,
.patient-image {
  max-width: 100px;
  height: auto;
  margin-bottom: 15px;
}

.patient-image {
  border-radius: 50%;
  border: 3px solid #2a3f54;
}

.info-card p {
  margin-bottom: 8px;
  color: #555;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

@media (max-width: 767px) {
  .accordion-button {
    background-color: #2a3f54;
    color: white;
  }

  .accordion-button:not(.collapsed) {
    background-color: #1ab89d;
    color: white;
  }

  .accordion-body {
    background-color: #f8f9fa;
  }

  .accordion {
    margin-top: 20px;
    margin-bottom: 20px;
    margin-left: 12px;
    margin-right: 12px;
  }
}
</style>
