<template>
  <div class="home">
    <div class="feature-card">
      <router-link to="/movie/tt3896198">

        <img src="https://image.api.playstation.com/vulcan/ap/rnd/202106/1704/JzL1NLQvok7Pghe9W5PP2XNV.png" alt="bleach" class="featured-img">
        <div class="detail">
          <h3>Bleach</h3>
          <p>A family is attacked by demons and only two members survive - Tanjiro and his sister Nezuko, 
            who is turning into a demon slowly. Tanjiro sets out to become a demon slayer to avenge his family and cure his sister.</p>
        </div>

      </router-link>
    </div>

    <form @submit.prevent="searchMovies()" class="search">
      <input type="text" placeholder="no forget press enter o" v-model="search">
      <input type="submit">
    </form>

    <div class="movie-list">
      <div class="movie" v-for="movie in movies" :key="movie.imdbd">

        <router-link to="/movie/tt3896198" class="movie-link">
              <div class="product">
                <img :src="movie.Poster" alt="">
                <div class="type">{{movie.Type}}</div>
              </div>
            <div class="detail">
              <p class="year">{{movie.year}}</p>
              <h3>{{movie.Title}}</h3>
            </div>
        </router-link>

      </div>

    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import {ref} from 'vue';
import env from '@/env.js'

export default {
  setup(){
    const search = ref("");
    const movies = ref([]);

    const searchMovies = ()=> {
      if(search.value !=''){
        fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&s=${search.value}`)
        .then(response => response.json())
        .then(data => {
          movies.value = data.Search;
          search.value = "";
          
        });
      }
    }
      return{
        search,
        movies,
        searchMovies
      }
  }
}
</script>
<style lang="scss">
*{
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

  .feature-card{
    position: relative;
    
    .featured-img{
      width: 100%;
     height: 60vh;
     object-fit:contain;
    }  
    
    .detail{
      position: absolute;
      left: 0%;
      right: 0%;
      bottom: 0%;
      background: rgba(0, 0, 0, 0.6);
      padding: 1rem;
      h3{
        margin-bottom: 1rem;
       color: #fff;
       
      }
      p{
        color: #fff;
        line-height: 1.5;

      }
    }
  }


  .search{
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 10px;

    input{
      border: none;
     

      &[type="text"]{
         width: 100%;
         height: 2rem;
         border-radius: 8px;
         transition: 0.4s;
         color: #42bb83;
         text-align: center;
         padding: 16px;
         margin-bottom: 1rem;
         background-color: aliceblue;
      }

      &[type="submit"]{
        color: #42bb83;
        width: 100%;
        padding: 16px;
        font-size: 20px;
        transition: 0.4s;
        background: #06110f;

        &:active{
          background: #228b5a;
        }
      }

    }

  }

  .movie-list{
    display: flex;
    flex-wrap: wrap;
    margin: 0px 8px;
    .movie{
      max-width: 50%;
      flex: 1 1 50%;
      padding: 16px 8px;

      .movie-link{
        display: flex;
        flex-direction: column;
        height: 100%;

        .product{
          position: relative;
          display: block;

          img{
            display: block;
            width: 100%;
            height: 275px;
            object-fit: cover;
          }

          .type{
            position: absolute;
            padding: 8px 16px;
            background:#42bb83;
            color: #fff;
            bottom: 16px;
            left: 0px;
            text-transform: capitalize;
          }
          .detail{
            background-color: #06110f;
            padding: 16px 8px;
            flex: 1 1 100%;
            border-radius: 0 0 8px 8px ;

            .year{
              color: #AAA;
              font-size: 14px;
            }

            h3{
              color: #fff;
              font-weight: 600;
              font-size: 18px;
            }
          }
        }
      }
    }
  }
</style>
