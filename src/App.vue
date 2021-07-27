<template>
  <div class="container">
    <div class="container_content">
      <h1 class="title">Comparison component</h1>
      <ComparisonSlider />
    </div>
  </div>
</template>

<script>
import ComparisonSlider from '@/components/ComparisonSlider.vue'

export default {
  name: 'App',
  components: {
    ComparisonSlider
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2e4a66;
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.container {
  width: 100%;
  height: 100vh;
  background: #f1f1f1;
  display: flex;
  flex-flow: column;
  justify-content: center;
  align-items: center;

  &_content {
    width: 50%;
    text-transform: uppercase;
    font-size: 1rem;
    
  }
}

@media screen and (max-width:1024px) {
  .container {
    width: 100%;
    height: 100vh;
    background: #f1f1f1;
    display: flex;
    flex-flow: column;
    justify-content: center;
    align-items: center;

    &_content {
      width: 90%;
      text-transform: uppercase;
      font-size: 0.7rem;
      
    }
  }
}
</style>
