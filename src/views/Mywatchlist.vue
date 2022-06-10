<template>
      <div class="movies-list">
        <div class="movie" v-for="movie in moviesData" :key="movie._id">
          <div
            :to="'/movie/' + movie._id"
            class="movie-link"
            @click="redirect(movie)"
          >
            <div class="product-image">
              <div class="images">
                <img
                  :src="'https://image.tmdb.org/t/p/original/' + movie.poster_path"
                  alt="Movie Poster"
                />
              </div>
              <div class="detail">
                <h2>{{ movie.title }} ({{ movie.date.substr(0, 4) }})</h2>
                <br />
                <p class="description">
                  {{ movie.overview.substr(0, 150) }}...
                </p>
                <br />
              </div>
            </div>
          </div>
        </div>
      </div>
</template>

<script>
// import axios from "axios";
import axios from "axios";
export default {
  name: "Mywatchlist",
  data: function () {
    return {
      moviesData: [],
    };
  },
  created() {
    axios
      .get("http://localhost:3000/movies/mylist")
      .then((response) => {
        // Do something if call succeeded
        console.log(response);
        this.moviesData = response.data;
      })
      .catch((error) => {
        // Do something if call failed
        console.log(error);
      });
  },
  methods: {
    redirect(res){
       this.$root.movi=res;
      // this.$root.over=res.overview.substring(0,Math.min(res.overview.length()-1),60);
        this.$router.replace({ name: "Movie_Detail" });
        //console.log(res);
    },
    update: function (mov) {
      this.$root.movi = mov;
    },
  },

};
</script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.home {
  text-align: center;
  /*background: linear-gradient(#1f1b1b, #ff0000);*/
  padding: 0px 0px;
  background-color: #161616;
}

h3 {
  margin: 40px 0 0;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}


.product-image:hover .product-image {
  transform: scale(1.2);
  transition: 300ms;
}

.movies-list {
  display: flex;
  flex-wrap: wrap;
  gap: 150px 50px;
  align-content: center;
  justify-content: center;
}

.product-image {
  width: 320px;
  margin: auto;
  height: 400px;
  transition: all 0.5s ease-in-out;
}

.product-image:hover {
  transform: scale(1.2) !important ;
}

.product-image:hover .images {
  transition: 0.5s !important ;
  opacity: 0.4 !important;
}

.detail {
  width: 260px !important ;
  position: relative !important;
  opacity: 0 !important ;
  transition : all 0.5s ease-in-out !important;
}

.product-image:hover .detail {
  opacity: 1 !important;
  color: rgb(255, 255, 255) !important;
  transition: 0.5s !important;
}

.detail {
  position: absolute !important;
  bottom: 20px !important;
  left: 0px !important ;
  opacity: 0 !important;
  transition: all 0.5s ease-in-out !important;
}
h4 {
  margin: 0px 0 0;
}
.most-popular {
  font-weight: 700;
  color: #ffffff;
  font-size: 30px;
  position: left;
}
input {
  display: block;
  width: 350px;
  margin: 20px auto;
  padding: 10px 45px;
  background-size: 15px 15px;
  font-size: 16px;
  border: none;
  border-radius: 5px;
  box-shadow: rgba(22, 22, 219, 0.25) 0px 2px 5px -1px,
    rgba(41, 34, 141, 0.3) 0px 1px 3px -1px;
}
.rating {
  font-weight: 700;
  color: #ff3939;
  font-size: 30px;
}
body{
  background-image:url("/back_ground.jpeg");
}
</style>
