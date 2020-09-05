<template>
  <div class="social">
    <!-- Bootstrap vue navbar -->
    <b-navbar toggleable="sm" type="light" variant="light">
      <b-navbar-toggle target="nav-text-collapse"></b-navbar-toggle>
      <!-- Emoji with route to / -->
      <b-navbar-brand>
        <nuxt-link class="navbar-brand" to="/"
          ><span style="font-size: 100px">&#128049;</span></nuxt-link
        >
      </b-navbar-brand>
      <!-- Router links with current page emphasized -->
      <b-collapse id="nav-text-collapse" is-nav>
        <b-navbar-nav>
          <nuxt-link class="nav-item nav-link" to="/"
            >Home<span class="sr-only">(current)</span></nuxt-link
          >
          <nuxt-link class="nav-item nav-link" to="/images"
            >Images<span class="sr-only">(current)</span></nuxt-link
          >
          <nuxt-link class="nav-item nav-link" to="/facts">Facts</nuxt-link>
          <nuxt-link class="nav-item nav-link active" to="/social"
            >Social<span class="sr-only">(current)</span></nuxt-link
          >
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>

    <!-- Page heading using named slot -->
    <div id="page-heading">
      <page-heading>
        <h1
          slot="page-title"
          class="font-weight-light text-center text-lg-left mt-4 mb-0"
          style="margin-left: 1rem"
        >
          Social
        </h1>
      </page-heading>
    </div>

    <!-- Bootstrap grid declaration -->
    <div class="row">
      <!-- v-if v-else implementation that changes image and text based on button toggle -->
      <div v-if="kittenMode" class="col-xl-8 col-lg-7 col-sm-6 col-12 p-5">
        <img
          :src="kittenSource"
          alt="Photo of cute gray kitten"
          class="img-fluid"
        />
        <p></p>
        <div class="text-center">
          <b-button variant="outline-primary" @click="kittenMode = !kittenMode"
            >Toggle Kitten Mode</b-button
          >
          <p class="text-success">{{ activatedText }}</p>
        </div>
      </div>
      <!-- v-else block -->
      <div v-else class="col-xl-8 col-lg-7 col-sm-6 col-12 p-5">
        <img
          :src="source"
          alt="Photo of two cats cuddling with each other"
          class="img-fluid"
        />
        <p></p>
        <div class="text-center">
          <b-button variant="outline-primary" @click="kittenMode = !kittenMode"
            >Toggle Kitten Mode</b-button
          >
          <p class="text-danger">{{ deactivatedText }}</p>
        </div>
      </div>
      <!-- Bootstrap grid item for page copy -->
      <div class="col-xl-4 col-lg-5 col-sm-6 col-12 p-5 text-center">
        <p class="lead">{{ heading }}</p>
        <p>{{ msg }}</p>
        <b-button pill :href="link">{{ btnText }}</b-button>
      </div>
    </div>

    <!-- Display Flickr content using array iteration and image card component -->
    <div class="flickrWrapper">
      <h4 class="flickrHeading">{{ flickrHeading }}</h4>
      <p v-if="loading" class="text-centered">Loading...</p>
      <div v-else class="masonry">
        <image-card v-for="image in images" :key="image.id" :image="image" />
      </div>
    </div>
  </div>
</template>

<script>
// Import axios and other components
import PageHeading from '@/components/PageHeading.vue'
import ImageCard from '@/components/ImageCard'
import axios from 'axios'

export default {
  name: 'Social',
  components: {
    PageHeading,
    ImageCard,
  },
  data() {
    return {
      heading: 'Meet Moon and Miu Miu',
      msg:
        "They're a long-haired tuxedo cat and Scottish Fold that grew up in New York City and currently reside in sunny Los Angeles, CA.",
      btnText: 'Follow on Instagram',
      source:
        'https://p46.f4.n0.cdn.getcloudapp.com/items/wbu7v7WY/moonandmiumiu.jpeg?source=viewer&v=2adb8019ffffe3997439f17a16da7cbe',
      kittenSource:
        'https://p46.f4.n0.cdn.getcloudapp.com/items/d5uEyEWE/IMG_0187.JPG?source=viewer&v=891f6f5ea4825336029a00f4f3795f93',
      link: 'https://www.instagram.com/moonandmiumiu/',
      kittenMode: false,
      activatedText: 'Kitten mode: Activated',
      deactivatedText: 'Kitten mode: Deactivated',
      loading: false,
      images: [],
      flickrHeading: 'Recent Flickr uploads',
    }
  },
  beforeMount() {
    this.loadImages()
  },
  methods: {
    loadImages() {
      this.loading = true
      this.fetchImages()
        .then((response) => {
          this.images = response.data.photoset.photo
          this.loading = false
        })
        .catch((error) => {
          console.log('An error ocurred: ', error)
        })
    },
    // Use axios to obtain images from Flickr. Hard coded api key and photoset id (which identifies a specific album)
    fetchImages() {
      return axios({
        method: 'get',
        url: 'https://api.flickr.com/services/rest',
        params: {
          method: 'flickr.photosets.getPhotos',
          api_key: 'd77d872ca3ee80854cc20e66d69ddf60',
          photoset_id: '72157715847390777',
          extras: 'url_n, url_o, owner_name, date_taken, views',
          page: 1,
          format: 'json',
          nojsoncallback: 1,
          per_page: 30,
        },
      })
    },
  },
}
</script>

<style lang="scss">
// Responsive styling for Flickr gallery
.flickrWrapper {
  margin: 1rem;
  max-width: 1200px;
  @media only screen and (max-width: 799px) {
    max-width: 100%;
    margin: 0 1.5rem;
  }
}

.masonry {
  margin: 1.5em auto;
  max-width: 1200px;
  column-gap: 1.5em;
}

@media only screen and (min-width: 1024px) {
  .masonry {
    column-count: 3;
  }
}

/* Masonry on medium-sized screens */
@media only screen and (max-width: 1023px) and (min-width: 768px) {
  .masonry {
    column-count: 2;
  }
}

/* Masonry on small screens */
@media only screen and (max-width: 767px) and (min-width: 540px) {
  .masonry {
    column-count: 1;
  }
}
</style>
