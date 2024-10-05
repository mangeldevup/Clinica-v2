<template>
  <nav class="navbar">
    <div class="container-nav">
      <button class="toggle-btn" aria-label="Toggle menu" @click="toggleMenu">
        <i class="bi bi-list"></i>
      </button>
    </div>
  </nav>
</template>

<script>
export default {
  name: "AppNavBar",
  methods: {
    toggleMenu() {
      this.$emit("toggle-menu");
    },
  },
};
</script>
