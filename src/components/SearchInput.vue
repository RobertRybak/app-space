<template>
  <input id="search" name="search" :value="value" @input="handleChange" />
</template>
<script>
export default {
  // eslint-disable-next-line quotes
  name: "SearchInput",
  props: {
    value: {
      type: String,
      required: true,
    },
  },
  methods: {
    handleChange(e) {
      // eslint-disable-next-line quotes
      this.$emit("input", e.target.value);
    },
  },
};
</script>

<style lang="scss" scoped>
label {
  font-family: Montserrot, sans-serif;
}
input {
  margin-top: 50px;
  display: flex;
  width: 250px;
  color: white;
  text-align: center;
  text-transform: uppercase;
  font-size: 18px;
  font-weight: 300;
  height: 30px;
  background: none;
  border: 0;
  border-bottom: 1px solid rgb(255, 255, 255);
  transition: box-shadow 0.3s ease-in;
  &:focus {
    outline: none;
    box-shadow: 0 10px 20px -8px rgba(255, 255, 255, 0.3);
  }

  @media (min-width: 1024) {
    font-weight: 400;
  }
}
</style>
