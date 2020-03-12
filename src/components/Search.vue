<template>
    <div class="searchWrapper">
        <div class="search">
            <input name="search" id="search">
        </div>
    </div>
</template>

<script>
export default {
  name: 'Search',
};
</script>

<style lang="scss" scoped>
  .search{
    display: flex;
    flex-direction: column;
    width: 260px;

    input{
      height: 30px;
      border: 0;
      border-bottom: 1px solid black;
      background: none;
    }
  }
</style>
