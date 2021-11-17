<template>
  <div class="wrapper">
    <HeroImage />
    <Claim />
    <SearchInput v-model="searchValue" @input="heandleInput" />
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
const API = "http://images-api.nasa.gov/search";
export default {
  // eslint-disable-next-line quotes
  name: "App",
  // eslint-disable-next-line quotes
  components: {
    HeroImage,
    Claim,
    SearchInput,
  },
  data() {
    return {
      // eslint-disable-next-line quotes
      searchValue: "",
      results: [],
    };
  },
  methods: {
    // eslint-disable-next-line func-names
    heandleInput: debounce(function () {
      console.log(this.searchValue);
      axios
        .get(`${API}?q=${this.searchValue}&media_type=image`)
        .then((response) => {
          this.results = response.data.collection.items;
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

.wrapper {
  width: 100%;
  min-height: 100vh;
  display: flex;
  padding: 30px;
  margin: 0;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
</style>
