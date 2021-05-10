<template>
  <section class="container">
    <div>
      <app-logo />
      <h1 class="title">my-vue</h1>
      <h2 class="subtitle">Nuxt.js project</h2>
      <p v-if="totalVuePackages.length === 0">Loading...</p>
      <div class="links">
        <ul id="example-1">
          <li v-for="(item, idx) in totalVuePackages" :key="idx">
            {{ item.package.name }} - {{ item.package.version }}
          </li>
        </ul>
      </div>
    </div>
  </section>
</template>

<script>
import AppLogo from "~/components/AppLogo.vue";

export default {
  components: {
    AppLogo,
  },
  data: function () {
    return { totalVuePackages: [] };
  },
  methods: {
    getPackages: async function () {
      const response = await fetch("https://api.npms.io/v2/search?q=vue");
      const data = await response.json();
      this.totalVuePackages = data.results;
    },
  },
  created() {
    this.getPackages();
  },
};
</script>

<style>
.container {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont,
    "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif; /* 1 */
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>

