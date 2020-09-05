<template>
  <div class="home">
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
          <nuxt-link class="nav-item nav-link active" to="/"
            >Home<span class="sr-only">(current)</span></nuxt-link
          >
          <nuxt-link class="nav-item nav-link" to="/images">Images</nuxt-link>
          <nuxt-link class="nav-item nav-link" to="/facts">Facts</nuxt-link>
          <nuxt-link class="nav-item nav-link" to="/social">Social</nuxt-link>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>

    <!-- Bootstrap jumbotron for main content -->
    <div class="jumbotron jumbotron-fluid">
      <div class="container">
        <h1 class="display-4 text-center"><span>&#128075;</span></h1>
        <p class="lead text-center">{{ msg }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Home',
  data() {
    return {
      msg: 'This site has been created using Nuxt, Vue, Vue Router, Bootstrap, and the Flickr API',
    }
  },
}
</script>
