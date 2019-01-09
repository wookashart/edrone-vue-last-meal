<template>
  <aside class="asideWrapper">
    <div class="tags-panel">
      <div class="tags-box">
        <h3>Category</h3>
        <div>
          <ul>
            <li v-for="(item, index) in this.tagging.uniqueCategory" :key="index">
              <div v-if="item">
                <span class="cancel-tag" @click="$emit('categoryCancel', item)">
                  <i class="fas fa-times-circle"></i>
                </span>
                <span>{{ item }}</span>
              </div>
            </li>
          </ul>
        </div>
      </div>
      <div class="tags-box">
        <h3>Area</h3>
        <div>
          <ul>
            <li v-for="(item, index) in this.tagging.uniqueArea" :key="index">
              <div v-if="item">
                <span class="cancel-tag" @click="$emit('areaCancel', item)">
                  <i class="fas fa-times-circle"></i>
                </span>
                <span>{{ item }}</span>
              </div>
            </li>
          </ul>
        </div>
      </div>
      <div class="tags-box">
        <h3>Tags</h3>
        <div>
          <ul>
            <li v-for="(item, index) in this.tagging.uniqueTags" :key="index">
              <div v-if="item">
                <span class="cancel-tag" @click="$emit('tagCancel', item)">
                  <i class="fas fa-times-circle"></i>
                </span>
                <span>{{ item }}</span>
              </div>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </aside>
</template>

<script>
export default {
  name: 'Aside',
  props: {
    tagging: {
      type: Object,
      required: true,
    }
  },
}
</script>

<style lang="scss" scoped>
  @import '../styles/colors';
  @import '../styles/mixins';

  .asideWrapper {
    background-color: $gray_dark;
    position: absolute;
    top: 0;
    left: 0;
    bottom: 0;
    width: 100vw;
    z-index: 10;
    transform: translateX(-100%);
    transition: 0.12s transform ease;

    @include media(desktop) {
      flex: 1;
      position: static;
      transform: none;
      transition: 0s;
    }

    &.open {
      transform: translateX(0);
    }
  }

  .tags-box {
    padding: 30px;

    > div {
      padding: 5px;
      margin-top: 15px;
      border: 1px solid $black;
      border-radius: 10px;
      min-height: 130px;

      ul {
        list-style: none;
        padding: 0;
        margin: 0;

        li {
          display: inline-block;
          font-size: 1.2rem;
          margin: 5px;

          > div {
            background-color: $white;
            padding: 5px;
            text-transform: uppercase;
            border-radius: 6px;
            color: $black;
          }

          span {
            display: inline-block;
          }

          .cancel-tag {
            display: inline-block;
            margin-right: 5px;
            cursor: pointer;
          }
        }
      }
    }
  }
</style>
