<template>
  <div class="item">
    <div :style="style" class="item" />
    <!-- <img :src="photo" :alt="title" > -->
  </div>
</template>

<script>
export default {
  name: 'Item',
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
  .item{
    min-width: 20vw;
    height: 250px;
    background-size: cover;
    background-repeat: no-repeat;
    background-position: 50%;
  }
</style>
