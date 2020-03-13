<template>
  <div class="backgroundImage" />
</template>

<script>
export default {
  name: 'BackgroundImage',
};
</script>

<style lang="scss" scoped>
.backgroundImage{
  position: fixed;
  z-index: -1;
  width: 100%;
  height: 100vh;
  background-image: linear-gradient(rgb(76, 43, 87), rgb(24, 24, 24));
}
.backgroundImage:after{
  content: '';
  opacity: 0.1;
  background: black;
  position: absolute;
  top: 0;
  left: 0;
  z-index: 1;
  width: 100%;
  height: 100vh;
}
</style>
