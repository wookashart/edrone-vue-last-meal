<template>
  <div class="navigationWrapper">
    <div class="content">
      <div class="hamburger-bar">
        <div>
          <i class="fas fa-bars"></i>
        </div>
      </div>
      <div class="search-bar">
        <label for="search">
          <i class="fas fa-search"></i>
        </label>
        <input name="search" id="search" placeholder="SEARCH" v-model="searchValue" @input="handleInput" />
      </div>
      <div class="favourites-bar">
        <div>
          <span>Favourites</span>
          <span><i class="far fa-heart"></i></span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import axios from 'axios';
  import debounce from 'lodash.debounce';

  const API = 'https://www.themealdb.com/api/json/v1/1/search.php';

  export default {
    name: 'Navigation',
    data() {
      return {
        searchValue: '',
        results: [],
      }
    },
    methods: {
      handleInput: debounce(function() {
        axios.get(`${API}?s=${this.searchValue}`)
          .then(response => {
            // this.results = response.data.collection.items;
            console.log(response);
          })
          .catch(err => {
            console.log(err);
          })
      }, 500)
    },
  }
</script>

<style lang="scss" scoped>
  @import '../styles/colors';

  .navigationWrapper {
    background-color: $yellow;
    padding: 5px 0;
  }

  .content {
    display: flex;
  }

  .hamburger-bar {
    flex: 1;
    font-size: 2.8rem;
    padding: 0 15px;
  }

  .search-bar {
    flex: 2;
    align-self: center;
    text-align: center;
    font-size: 2rem;
    padding: 0 15px;

    label {
      color: $gray;
      border: 1px solid $gray;
      border-right: 0;
      padding: 3px 10px 2px 7px;
      display: inline-block;
      vertical-align: middle;
      border-radius: 4px 0 0 4px;
    }

    input {
      height: 30px;
      width: calc(100% - 38px);
      border: 1px solid $gray;
      border-left: 0;
      background: transparent;
      outline: none;
      border-radius: 0 4px 4px 0;
    }
  }

  .favourites-bar {
    flex: 1;
    padding: 0 15px;

    > div {
      width: 100%;
      border: 1px solid $gray;
      border-radius: 4px;
      font-size: 1.6rem;
      text-transform: uppercase;
      color: $gray;
      padding: 5px;
      text-align: center;
      cursor: pointer;

      span {
        margin: 0 5px;
      }
    }
  }
</style>
