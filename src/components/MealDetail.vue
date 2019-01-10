<template>
  <div class="modal">
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
      <div class="close" @click="$emit('closeModal')" />
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
  @import '../styles/mixins';

  .modal {
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    margin: auto;
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: rgba(0, 0, 0, 0.3);
    z-index: 99999;
    overflow-y: scroll;
  }

  .information {
    width: 100%;
    border: 1px solid $gray;
    border-radius: 10px;
    overflow: hidden;
    display: flex;
    flex-flow: column;
    align-items: center;
    background-color: $white;
    box-shadow: 0 0 20px 10px rgba(0, 0, 0, 0.4);
    position: absolute;
    top: 0;
    left: 0;
    padding-top: 45px;

    @include media(desktop) {
      max-width: 60vw;
      flex-flow: row;
      position: relative;
      padding-top: 0;
    }

    .meal-info-img {
      width: 300px;
      height: 100px;
      position: relative;

      img {
        max-width: 300px;
        height: 100px;
        position: absolute;
        top: 0;
        bottom: 0;
        left: 0;
        right: 0;
        margin: auto;
      }

      @include media(desktop) {
        height: auto;
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

  .close {
    position: absolute;
    top: 10px;
    right: 15px;
    height: 20px;
    width: 20px;
    padding-top: 10px;
    cursor: pointer;

    &::before,
    &::after {
      content: '';
      display: block;
      width: 20px;
      height: 1px;
      background-color: $black;
    }

    &::before {
      transform: rotate(-45deg);
    }

    &::after {
      transform: rotate(45deg);
    }
  }
</style>
