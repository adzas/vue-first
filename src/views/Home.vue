<template>
  <div class="wrapper">
    <Claim />
    <Search />
  </div>
</template>

<script>
import debounce from 'lodash.debounce';
import Search from '@/components/Search.vue';
import Claim from '@/components/Claim.vue';

const API = 'https://images-api.nasa.gov/search?';

export default {
  name: 'Home',
  components: { Claim, Search },
  data() {
    return {
      searchValue: '',
      results: [],
    };
  },
  methods: {
    // eslint-disable-next-line
    handleInput: debounce(function () {
      this.axios.get(`${API}q=${this.searchValue}&media_type=image`).then((response) => {
        this.results = response.data.collection.items;
      }).catch((error) => {
        console.log(error);
      });
    }, 2000),
  },
};
</script>

<style lang="scss" scoped>
  .wrapper{
    margin: 0;
    width: 100%;
    padding: 30px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    background-image: linear-gradient(rgb(40, 28, 63), black);
    color: rgb(248, 234, 234);
  }
</style>
