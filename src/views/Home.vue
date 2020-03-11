<template>
  <div class="wrapper">
    <div class="search">
      <label for="search">Search</label>
      <input id="search" name="search" v-model="searchValue" @input="handleInput" />
      <ul>
        <li v-for="result in results" :key="result.data[0].nasa_id">
          <p>{{ result.data[0].description }}</p>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import debounce from 'lodash.debounce';

const API = 'https://images-api.nasa.gov/search?';

export default {
  name: 'Home',
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
    display: flex;
    flex-direction: column;
    align-items: center;
    margin: 0;
    padding: 30px;
    width: 100%;
  }

  .search{
    width: 260px;
    display: flex;
    flex-direction: column;

    label{
      font-family: Montserrat, sans-sefri;
    }

    input{
      height: 30px;
      border: 0;
      border-bottom: 1px solid black;

    }
  }
</style>
