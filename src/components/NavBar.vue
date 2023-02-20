<script setup>
import { RouterLink, RouterView } from "vue-router";
</script>
<script>
export default {
  data() {
    return { movieSearch: "" };
  },
};
</script>
<template>
  <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <RouterLink to="/" class="navbar-brand">Movies</RouterLink>
    <button
      class="navbar-toggler"
      type="button"
      data-toggle="collapse"
      data-target="#navbarSupportedContent"
      aria-controls="navbarSupportedContent"
      aria-expanded="false"
      aria-label="Toggle navigation"
    >
      <span class="navbar-toggler-icon"></span>
    </button>

    <div class="collapse navbar-collapse" id="navbarSupportedContent">
      <ul class="navbar-nav mr-auto">
        <li class="nav-item active">
          <RouterLink to="/" class="nav-link">
            Movies <span class="sr-only">(current)</span>
          </RouterLink>
        </li>
        <li class="nav-item">
          <RouterLink to="/about" class="nav-link">About</RouterLink>
        </li>
      </ul>
    </div>
  </nav>
  <RouterView />
</template>
