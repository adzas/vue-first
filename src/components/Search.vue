<template>
  <div class="search">
    <input
      id="search"
      name="search"
      :class="{ dark }"
      :value="value"
      @input="handleChange"
    >
  </div>
</template>

<script>
export default {
  name: 'Search',
  props: {
    value: {
      type: String,
      required: true,
    },
    dark: {
      type: Boolean,
      default: false,
    },
  },
  methods: {
    handleChange(event) {
      this.$emit('input', event.target.value);
    },
  },
};
</script>

<style lang="scss" scoped>
  $color: rgb(248, 234, 234);
  .search{
    margin-top: 1.5em;
    display: flex;
    flex-direction: column;
    width: 260px;

    @media (min-width: 768px) {
      width: 300px;
    }

    input{
      color: white;
      text-align: center;
      font-size: 20px;
      height: 40px;
      border: 0;
      border-bottom: 1px solid $color;
      background: none;
      transition: box-shadow .3s ease-out;

      @media (min-width: 768px) {
        font-size: 30px;
      }
    }

    input:focus{
      outline: none;
      box-shadow: 0 13px 15px -15px rgba(255, 255, 255, 0.6);
      /* box-shadow: 0 10px 20px -8px rgba(255, 255, 255, 0.301); */
    }
  }

  .dark{
    color: #1e3d4a !important;
    border-bottom-color: #1e3d4a !important;
  }

  .dark:focus{
    box-shadow: 0 10px 20px -8px #1e3d4a05 !important;
  }
</style>
