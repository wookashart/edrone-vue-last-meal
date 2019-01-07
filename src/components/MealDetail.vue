<template>
  <div class="information">
    <div v-if="this.selectedMeal.youtubeCode !== null">
      <iframe width="300" height="300" :src="'https://www.youtube.com/embed/' + this.selectedMeal.youtubeCode" frameborder="0" allow="accelerometer; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
    </div>
    <div v-else class="meal-info-img">
      <img :src="this.selectedMeal.strMealThumb" />
    </div>
    <div class="meal-details">
      <h3>Instruction</h3>
      <p>{{ this.selectedMeal.strInstructions }}</p>
      <h3>Ingredients + Measure</h3>
      <div class="meal-ingr-measure">
        <ul v-if="this.selectedMeal.idMeal !== ''">
          <li v-for="(value, index) in selectedMeal.ingredients" :key="index">{{ value }}</li>
        </ul>
        <ul v-if="this.selectedMeal.idMeal !== ''">
          <li v-for="(value, index) in selectedMeal.measure" :key="index">{{ value }}</li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MealDetail',
  props: {
    selectedMeal: {
      Type: Object,
      required: true,
    }
  },
}
</script>

<style lang="scss" scoped>
  @import '../styles/colors';

  .information {
    width: 100%;
    border: 1px solid $gray;
    margin: 20px;
    border-radius: 10px;
    overflow: hidden;
    display: flex;
    flex-flow: row;
    align-items: center;

    .meal-info-img {
      width: 300px;
      position: relative;

      img {
        max-width: 300px;
        position: absolute;
        top: 0;
        bottom: 0;
        left: 0;
        right: 0;
        margin: auto;
      }
    }

    .meal-details {
      padding: 20px;
      flex: 1;

      .meal-ingr-measure {
        display: flex;
        flex-flow: row;

        ul {
          padding: 0;
          list-style: none;
          margin-right: 20px;
        }
      }
    }
  }
</style>
