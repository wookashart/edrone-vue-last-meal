<template>
  <aside class="asideWrapper">
    <div class="tags-panel">
      <div class="tags-box">
        <h3>Category</h3>
        <div>
          <ul>
            <li>Vegetarian</li>
            <li>Food</li>
            <li>Deser</li>
          </ul>
        </div>
      </div>
      <div class="tags-box">
        <h3>Area</h3>
        <div>
          <ul>
            <li>Poland</li>
            <li>Cracov</li>
            <li>Berlin</li>
          </ul>
        </div>
      </div>
      <div class="tags-box">
        <h3>Tags</h3>
        <div>
          <ul>
            <li>Vegetarian</li>
            <li>Food</li>
            <li>Poland</li>
          </ul>
        </div>
      </div>
    </div>
  </aside>
</template>

<script>
export default {
  name: 'Aside',
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
          background-color: white;
          padding: 5px;
          text-transform: uppercase;
          border-radius: 6px;
          color: $black;
          margin: 5px;
        }
      }
    }
  }
</style>
