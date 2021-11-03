/* eslint-disable quotes */
/* eslint-disable quotes */
<template>
  <div class="wrapper">
    <Claim />
    <SearchInput />
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
const API = "http://images-api.nasa.gov/search";
export default {
  // eslint-disable-next-line quotes
  name: "Search",
  // eslint-disable-next-line quotes
  components: {
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
    heandlerInput: debounce(function () {
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
<style lang="scss" scoped>
.wrapper {
  width: 100%;
  height: 100vh;
  display: flex;
  padding: 30px;
  margin: 0;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background-image: url("../assets/heroimage.jpg");
  background-repeat: no-repeat;
  background-size: cover;
  background-position: 80% 0;
}
</style>
