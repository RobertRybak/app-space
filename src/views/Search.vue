/* eslint-disable quotes */
<template>
  <div class="wrapper">
    <div class="search">
      <label for="search">Search</label>
      <input
        id="search"
        name="search"
        type="text"
        v-model="searchValue"
        @input="heandlerInput"
      />

      <ul>
        <li v-for="item in results" :key="item.data[0].nasa_id">
          <p>{{ item.data[0].description }}</p>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
// eslint-disable-next-line quotes
import axios from "axios";
// eslint-disable-next-line quotes
import debounce from "lodash.debounce";

// eslint-disable-next-line quotes
const API = "http://images-api.nasa.gov/search";
export default {
  // eslint-disable-next-line quotes
  name: "Search",
  data() {
    return {
      // eslint-disable-next-line quotes
      searchValue: "",
      results: [],
    };
  },
  methods: {
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
  display: flex;
  padding: 30px;
  margin: 0;
  flex-direction: column;
  align-items: center;
}
.search {
  display: flex;
  flex-direction: column;
  width: 250px;
}
.search label {
  font-family: Montserrot, sans-serif;
}
.search input {
  height: 30px;
  border: 0;
  border-bottom: 1px solid black;
}
</style>
