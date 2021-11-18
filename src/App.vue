/* eslint-disable vue/require-v-for-key */
<template>
  <div :class="[{ flexStart: step === 1 }, 'wrapper']">
    <transition name="slide">
      <img src="./assets/logo.svg" class="logo" v-if="step === 1" />
    </transition>
    <transition name="fade">
      <HeroImage v-if="step === 0" />
    </transition>
    <Claim v-if="step === 0" />
    <SearchInput
      v-model="searchValue"
      @input="heandleInput"
      :dark="step === 1"
    />
    <div class="results" v-if="results && !loading && step === 1">
      <Item
        v-for="item in results"
        :item="item"
        :key="item.data[0].nasa_id"
        @click.native="handleModalOpen(item)"
      />
    </div>
    <div class="loader" v-if="step === 1 && loading">
      <div></div>
      <div></div>
      <div></div>
      <div></div>
    </div>
    <Modal v-if="modalOpen" :item="modalItem" @closeModal="modalOpen = false" />
  </div>
</template>
<script>
// eslint-disable-next-line quotes
import axios from "axios";
// eslint-disable-next-line quotes
import debounce from "lodash.debounce";

// eslint-disable-next-line no-unused-vars
// eslint-disable-next-line quotes
import Claim from "@/components/Claim.vue";

// eslint-disable-next-line quotes
import SearchInput from "@/components/SearchInput.vue";

// eslint-disable-next-line quotes
import HeroImage from "@/components/HeroImage.vue";
// eslint-disable-next-line quotes
import Item from "@/components/Item.vue";
// eslint-disable-next-line quotes
import Modal from "@/components/Modal.vue";

// eslint-disable-next-line quotes
const API = "http://images-api.nasa.gov/search";
export default {
  // eslint-disable-next-line quotes
  name: "App",
  // eslint-disable-next-line quotes
  components: {
    HeroImage,
    Claim,
    SearchInput,
    Item,
    Modal,
  },
  data() {
    return {
      modalOpen: false,
      modalItem: null,
      loading: false,
      step: 0,
      // eslint-disable-next-line quotes
      searchValue: "",
      results: [],
    };
  },
  methods: {
    handleModalOpen(item) {
      this.modalOpen = true;
      this.modalItem = item;
    },
    // eslint-disable-next-line func-names
    heandleInput: debounce(function () {
      this.loading = true;
      console.log(this.searchValue);
      axios
        .get(`${API}?q=${this.searchValue}&media_type=image`)
        .then((response) => {
          this.results = response.data.collection.items;
          this.loading = false;
          this.step = 1;
        })
        .catch((err) => {
          console.log(err);
        });
    }, 500),
  },
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Montserrat:wght@300;400;600;800&display=swap");

* {
  box-sizing: border-box;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

body {
  font-family: "Montserrat", sans-serif;
  margin: 0;
  padding: 0;
}
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.4s ease;
}
.fade-enter, .fade-leave-to
/* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
.slide-enter-active,
.fade-leave-active {
  transition: margin-top 0.4s ease;
}
.slide-enter, .slide-leave-to
/* .fade-leave-active below version 2.1.8 */ {
  margin-top: -50px;
}

.wrapper {
  width: 100%;
  min-height: 100vh;
  position: relative;
  display: flex;
  padding: 30px;
  margin: 0;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  &.flexStart {
    justify-content: flex-start;
  }
}
.logo {
  position: absolute;
  top: 30px;
}
.results {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-gap: 20px;
  margin-top: 50px;
  @media (min-width: 768px) {
    grid-template-columns: 1fr 1fr 1fr;
  }
}
.loader {
  display: inline-block;
  position: relative;
  width: 80px;
  height: 80px;
}
.loader div {
  box-sizing: border-box;
  display: block;
  position: absolute;
  width: 64px;
  height: 64px;
  margin: 8px;
  border: 8px solid #1e3d4a;
  border-radius: 50%;
  animation: loading 1.2s cubic-bezier(0.5, 0, 0.5, 1) infinite;
  border-color: #1e3d4a transparent transparent transparent;
}
.loader div:nth-child(1) {
  animation-delay: -0.45s;
}
.loader div:nth-child(2) {
  animation-delay: -0.3s;
}
.loader div:nth-child(3) {
  animation-delay: -0.15s;
}
@keyframes loading {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>
