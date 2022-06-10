<template>
  <div class="erra"
  :style="{
    'background-image': `url(netflix-gradient.png)`
  }"
>
  <div class="add">
    <h2>Add a movie</h2>
    <form>
      <label>Title</label>
      <input class="shadow appearance-none border rounded w-full py-2 px-3 text_ leading-tight focus:outline-none focus:shadow-outline" v-model="title" type="text">
      <label>overview</label>
      <input class="shadow appearance-none border rounded w-full py-2 px-3 text_ leading-tight focus:outline-none focus:shadow-outline" v-model="overview" type="text">
      <label>Poster path</label>
      <input class="shadow appearance-none border rounded w-full py-2 px-3 text_ leading-tight focus:outline-none focus:shadow-outline" v-model="poster_path" type="text">
      <label>Release Date</label>
      <input class="shadow appearance-none border rounded w-full py-2 px-3 text_ leading-tight focus:outline-none focus:shadow-outline" v-model="release_date" type="text">
      <label>Type</label>
      <div class="genre-selector">
        <button
          v-for="genre in dictGenres"
          :key="genre.id"
          type="button"
          @click="addGenre(genre)"
          class="btn btn-blue"
          :class="genre_ids.includes(genre.id) ?'yes':'no'">
          {{ genre.name }}
        </button>
      </div>
    </form>
      <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded-full" type="button" @click="envoie">Submit</button>
  </div>
</div>
</template>
<script>
import axios from "axios";
export default {
  name: "Add",
  created() {},
  data: function () {
    return {
      errors: [],
      title: null,
      date: "",
      backdrop_path:null,
      genre_ids: [],
      vote_average: null,
      poster_path:"",
      overview:"",
      added: false,
      popularity: null,
      viewers: [],
      dictGenres: [
        {
          id: 28,
          name: "Action",
        },
        {
          id: 12,
          name: "Adventure",
        },
        {
          id: 16,
          name: "Animation",
        },
        {
          id: 35,
          name: "Comedy",
        },
        {
          id: 80,
          name: "Crime",
        },
        {
          id: 99,
          name: "Documentary",
        },
        {
          id: 18,
          name: "Drama",
        },
        {
          id: 10751,
          name: "Family",
        },
        {
          id: 14,
          name: "Fantasy",
        },
        {
          id: 36,
          name: "History",
        },
        {
          id: 27,
          name: "Horror",
        },
        {
          id: 10402,
          name: "Music",
        },
        {
          id: 9648,
          name: "Mystery",
        },
        {
          id: 10749,
          name: "Romance",
        },
        {
          id: 878,
          name: "S-F",
        },
        {
          id: 10770,
          name: "TV Movie",
        },
        {
          id: 53,
          name: "Thriller",
        },
        {
          id: 10752,
          name: "War",
        },
        {
          id: 37,
          name: "Western",
        },
      ],
  };
},
  methods: {
    addGenre: function (genre) {
      if (!this.genre_ids.includes(genre.id)) {
        this.genre_ids.push(genre.id);
      }
      else{
        this.genre_ids.splice(this.genre_ids.indexOf(genre.id),1);
      }
    },
    envoie: function () {
      // this.checkForm();
      if (this.errors.length == 0) {
        axios
          .post(`http://localhost:3000/movies/new`, {
            title: this.title,
            poster_path:this.poster_path,
            backdrop_path:null,
            adult:false,
            genre_ids: this.genre_ids,
            release_date: this.release_date,
            overview:this.overview,
            vote_average: null,
            popularity: null,
            viewers: [],
          })
          .then((response) => {
            this.added = true;
            response.json("Movie added");
            console.log("Movie added");
          })
          .catch((error) => {
            this.moviesLoadingError = "An error occured while fetching movies.";
            console.log(error);
          });
      }
    },
    checkForm: function () {
      this.errors = [];
      if (!this.title) this.errors.push("title required.");
      if (!this.date) this.errors.push("day required.");
      if (!this.month) this.errors.push("month required.");
      if (!this.year) this.errors.push("year required.");
      if (this.genre_ids.length == 0) this.errors.push("genre required");
    },
  },
  // },

}
  //   submit: function () {
  //     axios
  //       .post(`${process.env.VUE_APP_BACKEND_BASE_URL}/movies/new`, {
  //         title: this.title,
  //         overview: this.overview,
  //         release_date: this.release_date,
  //         poster_path: this.poster_path,
  //         genre_ids: this.genres,
  //         average_rating: 0,
  //       })
  //       .then((response) => {
  //         console.log("on submit:", response);
  //         window.location.href = "/details?id=" + response.data._id;
  //       })
  //       .catch((error) => {
  //         console.log(error);
  //       });
  //   },
</script>

<style scoped>
.genre {
  display: flex;
  font-size: 1em;
  border-radius: 10px;
  padding: 5px;
  margin: 5px;
  transition: 0.4s;
  align-items: center;
}
.add {
  display: flex;
  flex-direction: column;
  align-items: center;
}
h2 {
  text-align: left;
  color:white;
  font-size: 2.3em;
  margin-top: 100px;
}
form {
  display: flex;
  flex-direction: column;
  width: 20%;
  min-width: 300px;
  margin: 50px;
}
input,
textarea {
  margin: 10px;
  margin-bottom: 20px;
}
textarea {
  height: 100px;
}
label {
  color: white;
  font-size: 1.3em;
}
button {
  margin: 10px 5px 10px 5px;
  width: 150px;
}

.btn {
  @apply font-bold py-2 px-4 rounded;
}
.btn-blue {
  @apply bg-blue-500 text-white;
}
.btn-blue:hover {
  @apply bg-blue-700;
}
.yes{
  @apply bg-red-700;
}
.no{
  @apply bg-blue-500;
}
.erra{
  background-size:cover;
}

</style>
