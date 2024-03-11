<template>
  <div id="app">
    <Header />
    <div class="container">
			<Main />
    </div>
    <Footer />
  </div>
</template>

<script>
import Vue from 'vue';
// import Header from "./components/layout/Header.vue";
import Footer from "./components/layout/Footer.vue";
import Main from "./components/forms/IpipMain.vue";

Vue.mixin({
  data: function() {
    return {
      questionsNumber: 30
    }
  }
})

export default {
  name: "app",
  components: {
    Main
  }
};
</script>