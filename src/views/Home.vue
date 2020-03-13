<template>
  <div :class="[{ flexStart: step === 1 }, 'wrapper']">
    <transition name="head">
      <h2 class="head" v-if="step === 1">-SPACER-</h2>
    </transition>
    <transition name="fade">
      <BackgroundImage v-if="step === 0"/>
    </transition>
    <Claim v-if="step === 0" />
    <Search v-model="searchValue" @input="handleInput" :dark="step === 1"/>
    <div class="results" v-if="results && !loading && step === 1">
      <!-- <div v-for="item in results" :key="item.data[0].nasa_id" >
        <p>{{ item.links[0] }}</p>
      </div> -->
      <Item v-for="item in results" :item="item" :key="item.data[0].nasa_id" />
    </div>
  </div>
</template>

<script>
import debounce from 'lodash.debounce';
import BackgroundImage from '@/components/BackgroundImage.vue';
import Claim from '@/components/Claim.vue';
import Search from '@/components/Search.vue';
import Item from '@/components/Item.vue';

const API = 'https://images-api.nasa.gov/search?';

export default {
  name: 'Home',
  components: {
    Claim,
    Search,
    BackgroundImage,
    Item,
  },
  data() {
    return {
      loading: false,
      step: 0,
      searchValue: '',
      results: [],
    };
  },
  methods: {
    // eslint-disable-next-line
    handleInput: debounce(function () {
      if (this.searchValue.length > 0) {
        this.loading = true;
        this.axios.get(`${API}q=${this.searchValue}&media_type=image`).then((response) => {
          this.results = response.data.collection.items;
          this.loading = false;
          this.step = 1;
        }).catch((error) => {
          console.log(error);
        });
      } else {
        this.step = 0;
      }
    }, 500),
  },
};
</script>

<style lang="scss" scoped>
  $color: rgb(248, 234, 234);

  .fade-enter-active, .fade-leave-active{
    transition: opacity .5s ease;
  }

  .fade-enter, .fade-leave-to{
    opacity: 0;
  }

  .head{
    color: black;
    position: absolute;
    margin-top: -10px;
  }

  .results{
    margin-top: 25px;
    color: black;
    width: 100%;
    display: grid;
    grid-template-columns: 1fr;
    grid-gap: 20px;

    @media(min-width: 512px) {
      grid-template-columns: 1fr 1fr;
    }
    @media(min-width: 768px) {
      grid-template-columns: 1fr 1fr 1fr;
    }
    @media(min-width: 1024px) {
      grid-template-columns: 1fr 1fr 1fr 1fr;
    }
  }

  .head-enter-active, .head-leave-active{
    transition: margin-top .5s ease;
  }

  .head-enter, .head-leave-to{
    margin-top: -50px;
  }

  .wrapper{
    margin: 0;
    position: relative;
    width: 100%;
    min-height: 100vh;
    padding: 30px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    color: $color;

    h2{
      font-weight: 400;
      font-size: 13px;
      letter-spacing: 10px;
    }

    &.flexStart{
      justify-content: flex-start;
    }
  }
</style>
