<template>
  <div class="container">
    <LayoutHeader />
    <main>
      <router-view />
    </main>
    <LayoutFooter />
  </div>
</template>

<script>
import LayoutHeader from "./components/LayoutHeader.vue";
import LayoutFooter from "./components/LayoutFooter.vue";

export default {
  components: {
    LayoutHeader,
    LayoutFooter,
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Montserrat&family=Source+Sans+Pro&display=swap");
:root {
  --clr-primary-inactive: rgba(106, 28, 195, 0.38);
  --clr-primary: #6a1cc3;
  --clr-secondary: #8849cf;
  --clr-dark-purple: #4b148a;
  --clr-text: rgba(0, 0, 0, 0.87);
  --clr-surface: #fbfbfb;
  font-family: "Source Sans Pro", sans-serif;
  font-size: 14px;
  scroll-behavior: smooth;
}
html {
  background-color: var(--clr-surface);
}

html,
body {
  height: 100%;
}

main {
  display: flex;
  flex-direction: column;
  margin: 0 auto;
  padding: 0.5rem;
  max-width: 700px;
}

h1,
h2,
h3,
h4,
h5,
label {
  font-family: "Montserrat", sans-serif;
  margin: 0;
}

p {
  margin: 0;
  padding: 0;
}
</style>
