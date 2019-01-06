<template>
  <div class="home">
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
    <div class="content main-box">
      <Aside />
      <Content :results="results" />
    </div>
  </div>
</template>

<script>
import Aside from '@/components/Aside';
import Content from '@/components/Content';

import axios from 'axios';
import debounce from 'lodash.debounce';

const searchAPI = 'https://www.themealdb.com/api/json/v1/1/search.php';
const latestMealsAPI = 'https://www.themealdb.com/api/json/v1/1/latest.php';

export default {
  name: 'home',
  data() {
    return {
      searchValue: '',
      results: [],
    }
  },
  components: {
    Aside,
    Content,
  },
  methods: {
    handleInput: debounce(function() {
      axios.get(this.searchValue !== '' ? `${searchAPI}?s=${this.searchValue}` : latestMealsAPI)
        .then(response => {
          this.results = response.data.meals;
        })
        .catch(err => {
          console.log(err);
        });
    }, 500)
  },

  beforeMount() {
    axios.get(latestMealsAPI)
      .then(response => {
        this.results = response.data.meals;
      })
      .catch(err => {
        console.log(err);
      })
  }
};
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

  .main-box {
    display: flex;
  }
</style>
