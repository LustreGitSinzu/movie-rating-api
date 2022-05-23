<template>
  <header>
    <router-link to="/">
      <h1><span>MOVIE</span> RATING</h1>
    </router-link>
  </header>

<main>
  <router-view/>
</main>
</template>

<style lang="scss">

*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: sans-serif;

  &::selection{
    background: transparent(#42bb83, 0.5);

  }

  body{
    background: #071311;
  }
header{
  display: flex;
  align-items: center;
  justify-content: center;
  background: #06110f;
  a{
    text-decoration: none;
    color: aliceblue;
    padding:10px;

    h1{
      font-size: large;

      span{
        color: #42bb83;
      }
    }

  }
}




}


</style>
