<template>
  <div class="claimWrapper">
    <h1 class="claim">SPACER</h1>
    <p class="subclaim">
      Interdum vivamus sollicitudin cursus eget accumsan placerat lorem tristique
      vivamus vel purus eu suspendisse suspendisse lorem vel ex mi congue
      lorem ac nunc tempus maecenas.
    </p>
    <p class="subclaim">
      Condimentum massa lorem lorem magna quisque suspendisse eget purus quam tristique proin.
    </p>
  </div>
</template>

<script>
export default {
  name: 'Claim',
};
</script>

<style lang="scss" scoped >

  .claimWrapper{
    width: 260px;
    text-align: center;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;

    @media(min-width: 768px) {
      width: 600px;
    }
    @media (min-width: 1024px) {
      width: 800px;
    }

    .claim{
      font-size: 50px;
      margin: 0;

      @media (min-width: 768px) {
        font-size: 80px;
      }
      @media (min-width: 1024px) {
        font-size: 100px;
      }
    }

    .subclaim{
      margin: 20px 0 0 0;
      font-size: 13px;
      font-weight: 400;

      @media (min-width: 768px) {
        font-size: 17px;
      }
      @media (min-width: 1024px) {
        font-size: 20px;
        margin: 30px 0 0 0;
      }
    }
  }

</style>
