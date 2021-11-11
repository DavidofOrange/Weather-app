<template>
  <div> 
    <h1 id="title">Weather-App</h1>
  </div>
</template>

<script>
export default {
  name: 'Title'
}
</script>

<style scoped>
  @import url('https://fonts.googleapis.com/css2?family=Lobster&display=swap');

  h1 {
    font-family: 'Lobster', cursive;
    text-align: center;
    text-shadow: 3px 2px 2px rgb(2, 2, 2);
    font-size: 80px;
    color: rgb(255, 255, 255);
    padding: 10px;
    margin: 10px;
  }

  @media only screen and (max-width: 600px) {
    h1 {
      font-size: 40px
    }
  }

  @media only screen and (max-width: 350px) {
    h1 {
      font-size: 25px
    }
  }
</style>