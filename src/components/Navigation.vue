<template>
  <div>
      <nav>
        <h1>Where in the world ?</h1>
        <!--
        <button class="mode-btn">
          Home
        </button>
        -->
      </nav>
  </div>
</template>

<script>
export default {
    name:'Navigation'
}
</script>

<style lang="scss" scoped>
nav{
  background: white;
  box-shadow: 0 0 10px 2px rgba($color: #000000, $alpha: 0.15);
  display: flex;
  justify-content: space-between;
  align-items: center;
  position: fixed;
  width: 100%;
  padding: 25px 5%;
  h1{
    font-weight: 900;
  }
}
.mode-btn{
  border: none;
  background: white;
  padding:8px 10px;
  font-size:1rem;
  font-family: 'Nunito Sans', sans-serif;
  font-weight:600;
  cursor: pointer;
  border: 1px solid black;
  border-radius: 5px;
  transition: all 0.3s ease;
  &:hover{
    background: black;
    color: white;
    transition: all 0.3s ease;
  }
}
</style>>