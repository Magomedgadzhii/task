<template>
  <div class="sidebar">
    <router-link class="sidebar__link" to="/">Задачи</router-link>
  </div>
</template>


<style lang="scss" scoped>
.sidebar {
  width: 25%;
  max-width: 200px;
  height: 100%;

  display: flex;
  flex-direction: column;
  align-items: center;

  background: #000;

  padding: 40px 0;
  &__link {
    font-size: 20px;
    color: #fff;
    text-decoration: none;
  }
  &__link:hover {
    color:blue;
  }


}


</style>
