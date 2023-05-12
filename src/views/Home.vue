
<template>

<div>
  <nav>
    <h1 class="header">Welcome To Movies!</h1>
    <input class="searchbar" type="text" placeholder="Search by movie name" v-model="text" @input="filteredList"/>
  </nav>
   
  <div class="content-box"> 
    <div class="allMovie">
      <h1 class="box-heading">Movies Name</h1>
      
      <div class="movie-section">
        <div class="list" v-for="movie in this.movies" :key="movie.id">
          <div class="img">
          <img :src="movie.poster" alt="photo">
          </div>
          <div class="title">
          {{movie.title}}
          </div>
          <div class="des">
          {{movie.overview}}
          </div>
          <button class="btn" @click = "favorite(movie) ">
           <i  class="fa fa-star icon" aria-hidden="true"></i>
           </button>
       </div>

      </div>
    </div>

    <div class="fav-filter">

      <div class="filteredMovie">
       <h1 class="box-heading">Filtered Movies</h1>
        <div class="movie-section-fil">

          <div class="list list-fil" v-for="movie in this.selectedMovies" :key="movie.id">
            <div class="img">
             <img :src="movie.poster" alt="photo">
            </div>
            <div class="title">
             {{movie.title}}
            </div>
            <div class="des">
              {{movie.overview}}
            </div>
            <button class="btn" @click = "favorite(movie)"><i class="fa fa-star icon" aria-hidden="true"></i></button>
          </div>
        </div>
      </div>

      <div class="favourite">
         <h1 class="box-heading">Favourite Movies</h1>
         <div class="movie-section-fil">
            <div class="list list-fil" v-for="movie in this.favouriteMovies" :key="movie.id">
              <div class="img">
              <img :src="movie.poster" alt="photo">
              </div>
              <div class="title">
              {{movie.title}}
              </div>
              <div class="des">
                {{movie.overview}}
              </div>
              <button class="btn" @click = "deletemovie(movie)"><i class="fa fa-star icon icon-fav " aria-hidden="true"></i></button>
            </div>
            </div>
      </div>
    </div>
  </div>
</div>

</template>

<script >

import axios from 'axios'
 

export default {
    name: 'home',
    mounted() {
        axios({
          method: "GET",
          "url": "assets/json/movies.json"
        }).then(response => {
          this.movies = JSON.parse(JSON.stringify(response.data));
        }, error => {
          // eslint-disable-next-line
          console.error(error);
        });
    },
    data() {
        return {

          movies:[],
          selectedMovies:[],
          favouriteMovies:[],
          text:""
        }
    },
    components: {},
    methods: {
      filteredList(event) {
        this.selectedMovies = this.movies.filter((movie) => {
          return movie.title.toLowerCase().includes(event.target.value.toLowerCase());
        });
      },

      favorite(event){
        if(!this.favouriteMovies.includes(event)){
            this.favouriteMovies.push(event);
          }
      },

      deletemovie(event){
        if(this.favouriteMovies.includes(event)){
          this.favouriteMovies.splice(this.favouriteMovies.indexOf(event), 1);
        }
      }
    }
}


</script>


<style scoped>

body{
  margin: 0;
  padding: 0;
}
::-webkit-scrollbar {
    display: none;
}

nav{
  display: flex;
  flex-direction: column;
  height: 10%;
  width: 91vw;
  background-color: rgb(66, 43, 43);
  margin: auto;
  padding: 1rem;
  align-items: center;
}

.header{
  color: white;
}
.searchbar{
   height: 2rem;
   width: 30rem;
}

 .content-box{
       position: relative;
       margin: 1rem 4.5rem 0rem;
       display: flex;
       flex-wrap: wrap;
       justify-content: center;
      background-color: white;

  }


  .allMovie{
    width: 45%;
    height: 80vh;
    margin:1rem;
  }

  .fav-filter{

    display: flex;
    flex-wrap:wrap;
    width: 45%;
    height: 80vh;
    margin:1rem;
  }
  .filteredMovie,.favourite{
    display: flex;
    flex-wrap: wrap;
    width: 100%;
    height: 50%;
  }

  .list{
    position: relative;
    padding: 10px;
    height: 50%;
    width: 50%;
    background-color: white;
    border: 1px solid black;
    align-items: center;
    text-align: start;
    overflow-y: hidden;
    overflow-x: hidden;
  }
  .list:hover{
    background-color: azure;
  }
  .list-fil{
      height: 100%;
      width: 50%;
  }


  .moviename{
     height:20%;
     width: 20%;
     

  }

  .icon:hover{
     color:goldenrod;
  }
  .box-heading{
    display: flex;
    align-items: center;
    width: 100%;
    height: 4rem;
    justify-content: center;
    align-items: center;
    border: 2px solid black;
  }
  .movie-section{
    display: flex;
    flex-wrap: wrap;
    overflow-y: scroll;
    padding: 0;
    width: 100%;
    height:87.5% ;
    border: 1px solid black;
    border-bottom: 2px solid black;
    border-top: 2px solid black;
  }
  .movie-section-fil{
  
    display: flex;
    flex-wrap: wrap;
    overflow-y: scroll;
    margin-top:-1rem;
    width: 100%;
    height:75% ;
    border: 1px solid black;
    border-bottom: 2px solid black;
    border-top: 2px solid black;
  }
  .btn{
    position: absolute;
    right: 4%;
    bottom:33%;
    background-color:q;
    height: 10%;
    width: 10%;
    margin: 0;
    padding: 0;
    cursor: pointer;
  }

  .icon{
    height: 60%;
    width: 60%;
  }
  .icon-fav{
    color:gold
  }
  .img{
    margin: 0;
    padding: 0%;
    height: 70%;
    width: 100%; 
  }
  img{
    height: 100%;
    width: 100%;
  }
  .title{
    height: 10%;
    text-decoration: underline;
    font-weight: bold;
    overflow: hidden;
    text-align: center;
    font-size: large;
    text-overflow: ellipsis;
    margin: 0.2rem;

  }
  .des{
    height: 14%;
    width: 100%;
    text-align: center;
    overflow:hidden;
    font-size:small;
    text-overflow: ellipsis;
    margin: 0.1rem;
    
  }
  
  
</style>

