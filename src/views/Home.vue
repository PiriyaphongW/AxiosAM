<template>
  <div>
    <!-- ค้นหา -->
    <div>
      <b-navbar toggleable="lg" type="dark" class="bgn" fixed="top">
        <router-link
          style="  text-decoration: none; color: rgb(255,215,0);  font-size: 30px; "
          to="/"
          >Japan Anime&Manga</router-link
        >
        <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

        <b-collapse id="nav-collapse" is-nav>
          <!-- Right aligned nav items -->
          <b-navbar-nav class="ml-auto">
            <b-form-input
              size="sm"
              class="mr-sm-2"
              placeholder="Search Anime Ex_Gon"
              v-model="query"
            ></b-form-input>
            <b-button
              size="sm"
              class="my-2 my-sm-0"
              type="submit"
              @click="handleSearchManga(manga)"
            >
              Search 
            </b-button>
          </b-navbar-nav>
        </b-collapse>
      </b-navbar>
    </div>

    <div style="background-image: url('https://dyrdkqpaj50j2.cloudfront.net/media/catalog/product/cache/29/image/9df78eab33525d08d6e5fb8d27136e95/l/i/light_orange-217-rsl-c.jpg');">
    <!-- slide -->
    <div >
      <b-carousel
        id="carousel-fade"
        style="text-shadow: 0px 0px 2px #000"
        fade
        indicators
        img-width="1024"
        img-height="480"
      >
        <b-carousel-slide
          caption=""
          img-src="https://wallpaperaccess.com/full/3565069.jpg"
        ></b-carousel-slide>
        <b-carousel-slide
          caption="Boku no Hero Academia"
          img-src="https://images4.alphacoders.com/819/thumb-1920-819837.png"
        ></b-carousel-slide>
        <b-carousel-slide
          caption="Your Name"
          img-src="https://images7.alphacoders.com/737/thumb-1920-737400.jpg"
        ></b-carousel-slide>
        <b-carousel-slide
          caption="Your Name"
          img-src="https://images4.alphacoders.com/973/thumb-1920-973967.jpg"
        ></b-carousel-slide>
      </b-carousel>
    </div>

   
    <!-- การ์ด -->
    <div class="my-5" >
      <div class="container" >
        <div class="row tt">
          <div
            class="col-md-3  d-flex align-items-stretch"
            v-for="manga in results"
            :key="manga.mal_id"
          >
            <b-card
              :title="manga.title"
              :img-src="manga.image_url"
              img-alt="Image"
              img-top
              tag="article"
              style="max-width: 20rem;"
              class="mb-2"
              @click="handleMangaClick(manga)"
            >
              <b-card-text>
                {{ manga.synopsis }}
              </b-card-text>

              <b-button href="#" variant="primary">Go somewhere</b-button>
            </b-card>
          </div>
        </div>
      </div>
    </div>
    </div>

  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      query: "",
      results: [],
    };
  },
  methods: {
    handleSearchManga() {
      const url = `https://api.jikan.moe/v3/search/manga?q=${this.query}&page=1`;
      axios.get(url).then((res) => {
        console.log(res);
        this.results = res.data.results;
      });
    },
    handleMangaClick(manga) {
      window.location = manga.url;
    },
  },
};
</script>

<style>
.tt {
  display: inline-flex;
}
.bgn {
  background-color: rgb(24, 82, 100);
}
</style>