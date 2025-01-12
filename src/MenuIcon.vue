<template>
  <svg
    xmlns="http://www.w3.org/2000/svg"
    width="24"
    height="24"
    viewBox="0 0 24 24"
    fill="none"
    :stroke="isActive ? 'red' : 'currentColor'" <!-- Dynamic color -->
    stroke-width="2"
    stroke-linecap="round"
    stroke-linejoin="round"
    class="menu-icon"
    @click="toggleState"
  >
    <line x1="3" y1="12" x2="21" y2="12"></line>
    <line x1="3" y1="6" x2="21" y2="6"></line>
    <line x1="3" y1="18" x2="21" y2="18"></line>
  </svg>
</template>

<script>
export default {
  name: "MenuIcon",
  data() {
    return {
      isActive: false, // Tracks the click state
    };
  },
  methods: {
    toggleState() {
      this.isActive = !this.isActive; // Toggle state
    },
  },
};
</script>

<style>
/* Default styles */
.menu-icon {
  cursor: pointer;
  transition: transform 0.3s ease, stroke 0.3s ease;
}

/* Add rotation or other transformations if active */
.menu-icon[stroke='red'] {
  transform: scale(1.2); /* Example: enlarge on click */
}
</style>
