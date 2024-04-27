<script setup>
import { RouterView } from 'vue-router'
import Navbar from "@/components/Navbar.vue";
import Footer from "@/components/Footer.vue";
import Preloader from "@/components/Preloader.vue";
</script>

<script>
export default {
  data(){
    return {
      theme: 'dark',
      loading: true,
    }
  },

  mounted() {
    setTimeout(() => {
      this.loading = false;
    }, 2000);

    if (localStorage.getItem("theme") == null) {
      localStorage.setItem("theme", "dark");
    } else {
      var element = document.getElementsByTagName("body")[0];
      element.setAttribute(
          "data-bs-theme",
          localStorage.getItem("theme")
      );
      this.theme = localStorage.getItem("theme");
    }
  },

  methods: {
    themeToggle() {
      var element = document.getElementsByTagName("body")[0];
      if (element.getAttribute("data-bs-theme") === "dark") {
        element.setAttribute("data-bs-theme", "light");
        this.theme = "light";
        localStorage.setItem("theme", "light");
      } else {
        element.setAttribute("data-bs-theme", "dark");
        this.theme = "dark";
        localStorage.setItem("theme", "dark");
      }
    },
  },
}
</script>

<template>
  <div class="d-flex flex-column justify-content-between position-relative" style="height: 100vh !important">
    <Transition name="fade">
      <Preloader v-if="loading"/>
    </Transition>

    <template v-if="!loading">
      <main class="flex-shrink-0" >
        <div
            v-if="theme === 'light'"
            @click="themeToggle"
            title="Change to Dark Mode"
            class="mode-toggle d-flex align-items-center justify-content-center"
        >
          <p class="mb-0" style="font-size: 28px">☀️</p>
        </div>

        <div
            v-else
            @click="themeToggle"
            title="Change to Light Mode"
            class="mode-toggle d-flex align-items-center justify-content-center"
        >
          <p class="mb-0" style="font-size: 28px">🌙</p>
        </div>

        <Navbar/>
        <Transition name="slide-fade">
          <RouterView />
        </Transition>
      </main>

      <Footer/>
    </template>
  </div>
</template>