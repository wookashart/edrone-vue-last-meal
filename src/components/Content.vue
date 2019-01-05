<template>
  <div class="contentWrapper">
    <div>
      <ul class="item-list">
        <li v-for="item in results" :key="item.idMeal">
          <div>
            <div :class="item.idMeal + ' thumb-box'" v-on:click="showDetail(item.idMeal)">
              <div class="thumb-img">
                <img :src="item.strMealThumb" />
              </div>
              <p>{{ item.strMeal }}</p>
            </div>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
  import axios from 'axios';

  const latestMealsAPI = 'https://www.themealdb.com/api/json/v1/1/latest.php';
  const findByIdAPI = 'https://www.themealdb.com/api/json/v1/1/lookup.php';

  export default {
    name: 'Content',
    data() {
      return {
        searchValue: '',
        results: [],
        mealDetail: {},
        boxClicked: false,
      }
    },
    methods: {
      showDetail: function(id) {
         axios.get(`${findByIdAPI}?i=${id}`)
          .then(response => {
            const allBoxes = [...document.querySelectorAll('.thumb-box')];

            this.mealDetail = response.data.meals[0];
            this.boxClicked = !this.boxClicked;

            if (this.boxClicked) {
              allBoxes.map(box => {
                box.style.opacity = "0.5";
              })
              document.getElementsByClassName(id)[0].style.opacity = "1";
            } else {
              allBoxes.map(box => {
                box.style.opacity = "1";
              })
            }
          })
          .catch(err => {
            console.log(err);
          })
      }
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
  }
</script>

<style lang="scss" scoped>
  @import '../styles/colors';

  .contentWrapper {
    flex: 3;
    padding: 15px 0;
  }

  .item-list {
    list-style: none;
    padding: 0;
    margin: 0;
    display: flex;
    flex-flow: row wrap;
    padding: 0 15px;

    li {
      width: calc(100% / 3);
      padding: 20px;
    }

    .thumb-box {
      border: 1px solid $gray;
      border-radius: 10px;
      overflow: hidden;
      cursor: pointer;
      transition: 0.1s opacity linear;

      .thumb-img {
        width: 100%;
        height: 200px;
        overflow: hidden;
        position: relative;

        img {
          max-width: 100%;
          position: absolute;
          top: 0;
          bottom: 0;
          left: 0;
          right: 0;
          margin: auto;
        }
      }

      > p {
        text-align: center;
        font-size: 1.2rem;
        color: $gray;
        margin: 0;
        padding: 15px 5px;
        text-transform: uppercase;
      }
    }
  }
</style>
