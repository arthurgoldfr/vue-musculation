<template>
  <div class="home">
  <img src="@/assets/musculation.jpg" alt="Snow" style="height:100%; width:100%">
  <h1 class="centered">
    Hello {{ user }}
  </h1>
  </div>
</template>

<style>
  div .home {
    position: relative;
    text-align: center;
    height: 100%;
    width: 100%;
  }
  .centered {
    color: white;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
  }

</style>

<script>

export default {
  name: 'Home',
    data() {
    return {
      user : "Jean"
    }
  }
}
</script>
