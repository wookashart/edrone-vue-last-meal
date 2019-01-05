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
        <input name="search" id="search" placeholder="SEARCH" />
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
export default {

}
</script>

<style lang="scss" scoped>
  .navigationWrapper {
    background-color: #FFFF8D;
    padding: 5px 0;
  }

  .content {
    display: flex;
  }

  .hamburger-bar {
    flex: 1;
    font-size: 3rem;
  }

  .search-bar {
    flex: 2;
    align-self: center;
    text-align: center;
    font-size: 2rem;

    label {
      color: #2D2D0F;
      border: 1px solid #2D2D0F;
      border-right: 0;
    }

    input {
      
    }
  }

  .favourites-bar {
    flex: 1;
  }
</style>

