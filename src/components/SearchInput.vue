<template>
  <div class="searchWrapper">
    <input
      id="search"
      name="search"
      type="text"
      v-model="searchValue"
      @input="heandlerInput"
    />
  </div>
</template>
<script>
export default {
  // eslint-disable-next-line quotes
  name: "SearchInput",
};
</script>

<style lang="scss" scoped>
.searchWrapper {
  margin-top: 50px;
  display: flex;
  flex-direction: column;
  width: 250px;
}
.searchWrapper label {
  font-family: Montserrot, sans-serif;
}
.searchWrapper input {
  background: none;
  height: 30px;
  border: 0;
  border-bottom: 1px solid black;
}
</style>
