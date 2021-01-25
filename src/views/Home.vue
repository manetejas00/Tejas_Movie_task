<template>
  <nav>
    <!--logo--------------->
    <a href="#" class="logo">
      <img src="../../test/images/logo.png" />
    </a>
    <!--menu--btn----------------->

    <!--menu-------------->
    <ul class="menu">
      <li><a href="#">Home</a></li>
      <li><a href="#">Movies</a></li>
      <li><a href="#">TV Shows</a></li>
      <li><a href="#">Hollywood</a></li>
      <li><a href="#">Horror</a></li>
    </ul>
    <!--search------------->
    <div class="search">
      <input
        type="text"
        placeholder="Find Your Favourtie Movies"
        v-model="search"
      />
      <form @submit.prevent="SearchMovies()" class="search-box">
        <input type="submit" value="Search" />
      </form>
      <!--search-icon----------->
      <i class="fa fa-search" aria-hidden="true"></i>
    </div>
    <div>
       <button
      type="button"
      class="btn-plus"
      @click="showModal"
    >
      +
    </button>

    <modal
      v-show="isModalVisible"
      @close="closeModal"
    />
    </div>
  </nav>
  <div class="home">
    <div class="feature-card">
      <router-link to="/movie/tt0409591"> </router-link>
    </div>
    <div class="slider">
      <section id="main">
        <!--showcase----------------------->
        <!--heading------------->
        <h1 class="showcase-heading">Showcase</h1>

        <ul id="autoWidth" class="cs-hidden">
          <!--box-1--------------------------->
          <li class="item-a">
            <!--showcase-box------------------->
            <div class="showcase-box">
              <img src="../../test/images/s-1.jpg" />
            </div>
          </li>
          <!--box-2--------------------------->
          <li class="item-b">
            <!--showcase-box------------------->
            <div class="showcase-box">
              <img src="../../test/images/s-2.jpg" />
            </div>
          </li>
          <!--box-3--------------------------->
          <li class="item-c">
            <!--showcase-box------------------->
            <div class="showcase-box">
              <img src="../../test/images/s-3.jpg" />
            </div>
          </li>
        </ul>
      </section>
    </div>
    <div class="slider">
      <section id="latest">
        <h2 class="latest-heading">Latest Movies</h2>
        <!--slider------------------->
        <ul id="autoWidth2" class="cs-hidden">
          <!--slide-box-1------------------>
          <li class="item-a">
            <div class="latest-box">
              <!--img-------->
              <div class="latest-b-img">
                <img src="../../test/images/m-1.jpg" />
              </div>
              <!--text---------->
              <div class="latest-b-text">
                <strong>Kin 2018</strong>
                <p>Action Movie</p>
              </div>
            </div>
          </li>
          <!--slide-box-2------------------>
          <li class="item-b">
            <div class="latest-box">
              <!--img-------->
              <div class="latest-b-img">
                <img src="../../test/images/m-2.jpg" />
              </div>
              <!--text---------->
              <div class="latest-b-text">
                <strong>Peninsula 2020</strong>
                <p>Action Movie</p>
              </div>
            </div>
          </li>
          <!--slide-box-3------------------>
          <li class="item-c">
            <div class="latest-box">
              <!--img-------->
              <div class="latest-b-img">
                <img src="../../test/images/m-3.jpg" />
              </div>
              <!--text---------->
              <div class="latest-b-text">
                <strong>Inception 2010</strong>
                <p>Action Movie</p>
              </div>
            </div>
          </li>

          <!--slide-box-4------------------>
          <li class="item-d">
            <div class="latest-box">
              <!--img-------->
              <div class="latest-b-img">
                <img src="../../test/images/m-4.jpg" />
              </div>
              <!--text---------->
              <div class="latest-b-text">
                <strong>Ironman 2008</strong>
                <p>Action Movie</p>
              </div>
            </div>
          </li>
          <!--slide-box-5------------------>
          <li class="item-e">
            <div class="latest-box">
              <!--img-------->
              <div class="latest-b-img">
                <img src="../../test/images/m-5.jpg" />
              </div>
              <!--text---------->
              <div class="latest-b-text">
                <strong>Venom 2018</strong>
                <p>Action Movie</p>
              </div>
            </div>
          </li>
          <!--slide-box-6------------------>
          <li class="item-f">
            <div class="latest-box">
              <!--img-------->
              <div class="latest-b-img">
                <img src="../../test/images/m-6.jpg" />
              </div>
              <!--text---------->
              <div class="latest-b-text">
                <strong>Aquaman 2018</strong>
                <p>Action Movie</p>
              </div>
            </div>
          </li>
          <!--slide-box-7------------------>
          <li class="item-g">
            <div class="latest-box">
              <!--img-------->
              <div class="latest-b-img">
                <img src="../../test/images/m-7.jpeg" />
              </div>
              <!--text---------->
              <div class="latest-b-text">
                <strong>Jungal Cruise 2018</strong>
                <p>Action Movie</p>
              </div>
            </div>
          </li>
        </ul>
      </section>
    </div>

    <section id="movies-list">
      <div class="movies-box" v-for="movie in movies" :key="movie.imdbID">
        <router-link :to="'/movie/' + movie.imdbID" class="movie-link">
          <div class="movies-img">
            <div class="quality">HDRip</div>
            <img :src="movie.Poster" alt="Movie Poster" />
            <div class="type">{{ movie.Type }}</div>
          </div>
          <a>
            {{ movie.Title }}
          </a>
        </router-link>
      </div>
    </section>
  </div>
</template>

<script>
import { ref } from "vue";
import env from "@/env.js";
import Modal from "../views/Modal"

export default {
  

   components: {
      Modal,
    },
     data () {
      return {
        isModalVisible: false,
      };
    },
    methods: {
      showModal() {
        this.isModalVisible = true;
      },
      closeModal() {
        this.isModalVisible = false;
      }
    },
  setup() {
    const search = ref("");
    const movies = ref([]);

    const SearchMovies = () => {
      if (search.value != "") {
        fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&s=${search.value}`)
          .then((response) => response.json())
          .then((data) => {
            movies.value = data.Search;
            search.value = "";
          });
      }
    };

    return {
      search,
      movies,
      SearchMovies,
    };
  },
};
</script>

<style>
.btn-plus{
   background-color: #4CAF50; /* Green */
  border: none;
  color: white;
  padding: 10px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  cursor: pointer;
  border-radius: 50%;
}
ul {
  list-style: none;
}
a {
  text-decoration: none;
}

nav {
  display: flex;
  justify-content: space-around;
  align-items: center;
  width: 100%;
  border: 1px solid rgba(0, 0, 0, 0.04);
  background-color: #ffffff;
  position: fixed;
  left: 0;
  top: 0;
  z-index: 100;
}
.logo img {
  height: 35px;
}
nav .menu {
  display: flex;
}

nav .menu li a {
  height: 40px;
  line-height: 43px;
  margin: 0px;
  padding: 0px 22px;
  display: flex;
  font-size: 0.8rem;
  text-transform: uppercase;
  font-weight: 500;
  color: #585858;
  letter-spacing: 1px;
}

.search {
  width: 250px;
  height: 40px;
  background-color: rgba(245, 245, 245, 0.8);
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 20px;
  padding: 0px 20px;
}
.search input {
  width: auto;
  height: 30px;
  border: none;
  outline: none;
  background-color: transparent;
}
.search i {
  color: #3a3a3a;
}
nav .menu li a:hover {
  background-color: #242424;
  color: #ffffff;
  box-shadow: 5px 10px 30px rgba(53, 53, 53, 0.1);
  transition: all ease 0.2s;
}

#main {
  padding-top: 80px;
  background-color: #ffffff;
}
.showcase-box {
  width: 430px;
  height: 250px;
  box-shadow: 5px 15px 30px rgba(0, 0, 0, 0.3);
  border-radius: 10px;
  margin: 0px 20px 10px 20px;
  overflow: hidden;
}
.showcase-box img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: top;
}

.cs-hidden {
  overflow: visible !important;
}
#latest {
  border-top: 1px solid rgba(53, 53, 53, 0.1);
}
.latest-heading {
  margin: 30px 30px 0px 30px;
  font-weight: 500;
  font-size: 1.3rem;
}
.latest-box {
  display: flex;
  flex-direction: column;
  align-items: center;
  box-shadow: 2px 2px 30px rgba(0, 0, 0, 0.2);
  margin: 20px 10px;
  border-radius: 10px;
  overflow: hidden;
  width: 200px;
  background-color: #ffffff;
}
.latest-b-img {
  width: 100%;
  height: 270px;
}
.latest-b-img img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
.latest-b-text strong {
  color: #3a3a3a;
  margin: 0px;
}
.latest-b-text {
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  margin: 10px;
}
.latest-b-text p {
  color: #979797;
  margin: 0px;
}
.movies-heading h2 {
  font-weight: 400;
  margin: 0px;
  padding: 1px 20px;
  background-color: rgba(0, 0, 0, 0.01);
  border: 1px solid rgba(0, 0, 0, 0.06);
  font-size: 1.7rem;
  letter-spacing: 1px;
  text-transform: uppercase;
  width: 100%;
}

#movies-list {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
}

.movies-box {
  width: 300px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-direction: column;
  box-shadow: 2px 2px 30px rgba(0, 0, 0, 0.2);
  margin: 20px;
  border-radius: 5px;
  overflow: hidden;
  border-top: 3px solid #292929;
}

.movies-img {
  width: 100%;
  height: 400px;
  position: relative;
}
.movies-img img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.movies-box a {
  text-align: center;
  display: block;
  font-weight: 600;
  display: -webkit-box;
  max-width: 80%;
  -webkit-line-clamp: vertical;
  overflow: hidden;
  text-overflow: ellipsis;
  color: #3a3a3a;
  margin: 20px;
}
.movies-box:hover {
  transform: translateY(-10px);
  transition: all ease 0.2s;
}
.slider {
  display: flex;
  justify-content: space-around;
  align-content: center;
}
.slider ul {
  display: flex;
}
</style>
