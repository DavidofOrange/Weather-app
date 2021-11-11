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
  h1 {
    text-align: center;
    text-shadow: 3px 2px 2px rgb(2, 2, 2);
    font-size: 50px;
    color: rgb(255, 255, 255);
    padding: 10px;
    margin: 10px;
  }
  @media only screen and (max-width: 500px) {
    h1 {
      font-size: 30px
    }
  }
  @media only screen and (max-width: 350px) {
    h1 {
      font-size: 20px
    }
  }
</style>