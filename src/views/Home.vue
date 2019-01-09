<template>
  <div class="home">
    <div class="navigationWrapper">
      <div class="content homeContent">
        <div class="hamburger-bar">
          <div @click="hamburgerClicked = !hamburgerClicked">
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
      <Aside
        :class="{ 'open' : hamburgerClicked }"
        :tagging="tagging"
        @categoryCancel="categoryCancel"
        @areaCancel="areaCancel"
        @tagCancel="tagCancel"
      />
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
      tagging: {},
      hamburgerClicked: false,
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

          this.setTagging();
        })
        .catch(err => {
          console.log(err);
        });
    }, 500),
    setTagging() {
      const area = [];
      const category = [];
      let tags = [];

      this.results.map(el => {
        area.push(el.strArea);
        category.push(el.strCategory);
        el.strTags !== null ? tags.push(el.strTags) : false;
      });
      tags = tags.join().split(',').sort();

      let uniqueCategory = category.filter((elem, index, self) => {
          return index == self.indexOf(elem);
      });

      let uniqueArea = area.filter((elem, index, self) => {
          return index == self.indexOf(elem);
      });

      let uniqueTags = tags.filter((elem, index, self) => {
          return index == self.indexOf(elem);
      });

      uniqueCategory = uniqueCategory.sort();
      uniqueArea = uniqueArea.sort();

      this.tagging = {
        uniqueArea,
        uniqueCategory,
        uniqueTags,
      };
    },
    categoryCancel(value) {
      const newResults = [];

      this.results.map(el => {
        if (el.strCategory !== value) {
          newResults.push(el);
        }
      });

      this.results = newResults;
      this.setTagging();
    },
    areaCancel(value) {
      const newResults = [];

      this.results.map(el => {
        if (el.strArea !== value) {
          newResults.push(el);
        }
      });

      this.results = newResults;
      this.setTagging();
    },
    tagCancel(value) {
      const newResults = [];

      this.results.map(el => {

        if (el.strTags === null || el.strTags.search(value) === -1) {
          newResults.push(el);
        }
      });

      this.results = newResults;

      this.setTagging();
    },
  },

  beforeMount() {
    axios.get(latestMealsAPI)
      .then(response => {
        this.results = response.data.meals;

        this.setTagging();
      })
      .catch(err => {
        console.log(err);
      })
  }
};
</script>

<style lang="scss" scoped>
  @import '../styles/colors';
  @import '../styles/mixins';

  .navigationWrapper {
    background-color: $yellow;
    padding: 5px 0;
  }

  .content {
    display: flex;
  }

  .homeContent {
    align-items: center;
  }

  .hamburger-bar {
    font-size: 2.8rem;
    padding: 0 10px;

    @include media(desktop) {
      flex: 1;
      padding: 0 15px;

      > div {
        display: none;
      }
    }
  }

  .search-bar {
    flex: 2;
    align-self: center;
    text-align: center;
    font-size: 1.7rem;
    padding: 0 10px;

    @include media(desktop) {
      padding: 0 15px;
    }

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
      color: $gray;
    }
  }

  .favourites-bar {
    padding: 0 10px;
    height: 30px;
    display: flex;

    @include media(desktop) {
      flex: 1;
      padding: 0 15px;
    }

    > div {
      display: flex;
      align-items: center;
      justify-content: center;
      width: 100%;
      border: 1px solid $gray;
      border-radius: 4px;
      font-size: 1.4rem;
      text-transform: uppercase;
      color: $gray;
      padding: 5px;
      text-align: center;
      cursor: pointer;

      span {
        margin: 0 5px;

        &:first-of-type {
          flex: 1;
          display: none;

          @include media(desktop) {
            display: inline-block;
          }
        }
      }
    }
  }

  .main-box {
    display: flex;
    position: relative;
  }

  @include media(desktop) {
    .leftSidebar-enter-active,
    .leftSidebar-leave-active {
      transform: translateX(0);
      transition: 0.12s ease;
    }

    .leftSidebar-enter,
    .leftSidebar-leave-to {
      transform: translateX(-100%);
    }
  }
</style>
