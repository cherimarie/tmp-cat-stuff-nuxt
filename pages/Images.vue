<template>
  <div class="images">
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
          <nuxt-link class="nav-item nav-link active" to="/images"
            >Images<span class="sr-only">(current)</span></nuxt-link
          >
          <nuxt-link class="nav-item nav-link" to="/facts">Facts</nuxt-link>
          <nuxt-link class="nav-item nav-link" to="/social">Social</nuxt-link>
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
          Cat photos
        </h1>
      </page-heading>
    </div>

    <!-- Gallery container using prop and iteration overy array of picture objects -->
    <section class="gallery-container">
      <div class="row text-center text-lg-left">
        <!-- Iteration over array of picture data objects defined in script data -->
        <div
          v-for="picture in pictures"
          :key="picture.link"
          class="col-lg-3 col-md-4 col-6"
        >
          <!-- Uses picture data prop defined in PictureData component -->
          <picture-data
            :link="picture.link"
            :src="picture.src"
            :alt="picture.alt"
          />
        </div>
      </div>
    </section>
  </div>
</template>

<script>
// Imports Heading and PictureData components
import PictureData from '@/components/PictureData.vue'
import PageHeading from '@/components/PageHeading.vue'

export default {
  // Registering imported components
  components: {
    PictureData,
    PageHeading,
  },
  data() {
    return {
      // Array declaration of picture objects
      pictures: [
        {
          link: 'https://source.unsplash.com/EnsRjlBwQsg/',
          src: 'https://source.unsplash.com/EnsRjlBwQsg/400x300',
          alt: 'Random photo of cat',
        },
        {
          link: 'https://source.unsplash.com/V7RugxejXH8/',
          src: 'https://source.unsplash.com/V7RugxejXH8/400x300',
          alt: 'Random photo of cat',
        },
        {
          link: 'https://source.unsplash.com/ZEd44nDPTfA/',
          src: 'https://source.unsplash.com/ZEd44nDPTfA/400x300',
          alt: 'Random photo of cat',
        },
        {
          link: 'https://source.unsplash.com/FT9SsFEXqF4/',
          src: 'https://source.unsplash.com/FT9SsFEXqF4/400x300',
          alt: 'Random photo of cat',
        },
        {
          link: 'https://source.unsplash.com/_STvosrG-pw/',
          src: 'https://source.unsplash.com/_STvosrG-pw/400x300',
          alt: 'Random photo of cat',
        },
        {
          link: 'https://source.unsplash.com/BMKtREjthyo/',
          src: 'https://source.unsplash.com/BMKtREjthyo/400x300',
          alt: 'Random photo of cat',
        },
        {
          link: 'https://source.unsplash.com/bGG85MrGV1o/',
          src: 'https://source.unsplash.com/bGG85MrGV1o/400x300',
          alt: 'Random photo of cat',
        },
        {
          link: 'https://source.unsplash.com/eFJfJkufGCU/',
          src: 'https://source.unsplash.com/eFJfJkufGCU/400x300',
          alt: 'Random photo of cat',
        },
        {
          link: 'https://source.unsplash.com/hjLueu0RbV8/',
          src: 'https://source.unsplash.com/hjLueu0RbV8/400x300',
          alt: 'Random photo of cat',
        },
        {
          link: 'https://source.unsplash.com/J8meHFhqSCM/',
          src: 'https://source.unsplash.com/J8meHFhqSCM/400x300',
          alt: 'Random photo of cat',
        },
        {
          link: 'https://source.unsplash.com/_VX-6amHgDY/',
          src: 'https://source.unsplash.com/_VX-6amHgDY/400x300',
          alt: 'Random photo of cat',
        },
        {
          link: 'https://source.unsplash.com/W8iQBo22Mp4/',
          src: 'https://source.unsplash.com/W8iQBo22Mp4/400x300',
          alt: 'Random photo of cat',
        },
      ],
    }
  },
  head() {
    return {
      title: 'Cat images',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'Random cat photos hosted on unsplash.com',
        },
      ],
    }
  },
}
</script>
