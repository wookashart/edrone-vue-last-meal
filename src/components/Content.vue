<template>
  <div class="contentWrapper">
    <div>
      <ul class="item-list">
        <li v-for="(item, index) in results" :key="item.idMeal">
          <div>
            <div :class="item.idMeal + ' thumb-box'" v-on:click="showDetail(item.idMeal, index)">
              <div class="thumb-img">
                <img :src="item.strMealThumb" />
              </div>
              <p>{{ item.strMeal }}</p>
            </div>
          </div>
        </li>
      </ul>
    </div>
    <MealDetail :selectedMeal="selectedMeal" v-if="boxClicked" @closeModal="boxClicked = false" />
  </div>
</template>

<script>
  import axios from 'axios';
  import MealDetail from '@/components/MealDetail';

  const findByIdAPI = 'https://www.themealdb.com/api/json/v1/1/lookup.php';

  export default {
    name: 'Content',
    data() {
      return {
        searchValue: '',
        mealDetail: {},
        boxClicked: false,
        selectedMeal: {},
        component: undefined,
      }
    },
    props: {
      results: {
        Type: Array,
        required: true,
      }
    },
    components: {
      MealDetail,
    },
    methods: {
      showDetail: function(id, index) {
        const boxList = [...document.querySelectorAll('.item-list li')];
        const infoBoxPosition = Math.ceil((index + 1) / 3) * 3;
        const allIngredients = [];
        const allMeasure = [];

        axios.get(`${findByIdAPI}?i=${id}`)
          .then(response => {
            const allBoxes = [...document.querySelectorAll('.thumb-box')];
            const youtubeUrl = this.results[index].strYoutube !== "" ? new URL(this.results[index].strYoutube) : null;
            const videoNumber = youtubeUrl !== null ? youtubeUrl.searchParams.get("v") : null;

            this.boxClicked = true;
            this.selectedMeal = this.results[index];
            this.selectedMeal.youtubeCode = videoNumber;

            for (let key in this.selectedMeal) {
              if (!key.search('strIngredient') && this.selectedMeal[key] !== "") {
                allIngredients.push(this.selectedMeal[key]);
              }

              if(!key.search('strMeasure') && this.selectedMeal[key] !== "") {
                allMeasure.push(this.selectedMeal[key]);
              }
            }

            this.selectedMeal.ingredients = allIngredients;
            this.selectedMeal.measure = allMeasure;
          })
          .catch(err => {
            console.log(err);
          })
      }
    },
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
