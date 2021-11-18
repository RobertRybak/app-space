/* eslint-disable vue/return-in-computed-property */
/* eslint-disable comma-dangle */
<template>
  <div :style="style" class="item"></div>
</template>

<script>
export default {
  // eslint-disable-next-line quotes
  name: "Item",
  props: {
    item: {
      type: Object,
      require: true,
    },
  },

  data() {
    return {
      photo: this.item.links[0].href,
      title: this.item.data[0].title,
    };
  },

  computed: {
    style() {
      return `background-image: url("${this.photo}")`;
    },
  },
};
</script>

<style lang="scss" scoped>
.item {
  width: 40vw;
  height: 250px;
  background-size: cover;
  background-repeat: no-repeat;
  @media (min-width: 768px) {
    width: 25vw;
  }
}
</style>
