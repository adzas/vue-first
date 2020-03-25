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
      <Item
        v-for="item in results"
        :item="item"
        :key="item.data[0].nasa_id"
        @click.native="handleModalOpen(item)"
      />
    </div>
    <div class="lds-roller" v-if="step === 1 && loading">
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
    </div>
    <Modal
      v-if="modalOpen"
      @closeModal="modalOpen = false"
      :item="modalItem"
    />
  </div>
</template>

<script>
import debounce from 'lodash.debounce';
import BackgroundImage from '@/components/BackgroundImage.vue';
import Claim from '@/components/Claim.vue';
import Search from '@/components/Search.vue';
import Item from '@/components/Item.vue';
import Modal from '@/components/Modal.vue';

const API = 'https://images-api.nasa.gov/search?';

export default {
  name: 'Home',
  components: {
    Claim,
    Search,
    BackgroundImage,
    Item,
    Modal,
  },
  data() {
    return {
      modalOpen: false,
      modalItem: null,
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
    handleModalOpen(item) {
      this.modalItem = item;
      this.modalOpen = true;
      console.log(Modal);
    },
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

  .lds-roller {
    margin-top: 20px;
    display: inline-block;
    position: relative;
    width: 80px;
    height: 80px;
  }
  .lds-roller div {
    animation: lds-roller 1.2s cubic-bezier(0.5, 0, 0.5, 1) infinite;
    transform-origin: 40px 40px;
  }
  .lds-roller div:after {
    content: " ";
    display: block;
    position: absolute;
    width: 7px;
    height: 7px;
    border-radius: 50%;
    background: black;
    margin: -4px 0 0 -4px;
  }
  .lds-roller div:nth-child(1) {
    animation-delay: -0.036s;
  }
  .lds-roller div:nth-child(1):after {
    top: 63px;
    left: 63px;
  }
  .lds-roller div:nth-child(2) {
    animation-delay: -0.072s;
  }
  .lds-roller div:nth-child(2):after {
    top: 68px;
    left: 56px;
  }
  .lds-roller div:nth-child(3) {
    animation-delay: -0.108s;
  }
  .lds-roller div:nth-child(3):after {
    top: 71px;
    left: 48px;
  }
  .lds-roller div:nth-child(4) {
    animation-delay: -0.144s;
  }
  .lds-roller div:nth-child(4):after {
    top: 72px;
    left: 40px;
  }
  .lds-roller div:nth-child(5) {
    animation-delay: -0.18s;
  }
  .lds-roller div:nth-child(5):after {
    top: 71px;
    left: 32px;
  }
  .lds-roller div:nth-child(6) {
    animation-delay: -0.216s;
  }
  .lds-roller div:nth-child(6):after {
    top: 68px;
    left: 24px;
  }
  .lds-roller div:nth-child(7) {
    animation-delay: -0.252s;
  }
  .lds-roller div:nth-child(7):after {
    top: 63px;
    left: 17px;
  }
  .lds-roller div:nth-child(8) {
    animation-delay: -0.288s;
  }
  .lds-roller div:nth-child(8):after {
    top: 56px;
    left: 12px;
  }
  @keyframes lds-roller {
    0% {
      transform: rotate(0deg);
    }
    100% {
      transform: rotate(360deg);
    }
  }
</style>
