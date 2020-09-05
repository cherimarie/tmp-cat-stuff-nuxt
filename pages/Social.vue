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

    <div class="flickrGallery"></div>
  </div>
</template>

<script>
import PageHeading from '@/components/PageHeading.vue'

export default {
  name: 'Social',
  components: {
    PageHeading,
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
      apiKey: 'd77d872ca3ee80854cc20e66d69ddf60',
      photoset: '72157715847390777',
    }
  },
}
</script>
