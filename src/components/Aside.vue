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

  .asideWrapper {
    background-color: $gray_dark;
    flex: 1;
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
