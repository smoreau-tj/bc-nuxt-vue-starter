<template>
  <header>
   <div class="header-left"></div>
   <div class="header-center">
     <nuxt-link to="/"><tjLogo /></nuxt-link>
   </div>
   <div class="header-right"></div>
    <h1 class="title">
      <tjLogo />
    </h1>
    <ul>
      <li>
        <nuxt-link to="/">
          Home
        </nuxt-link>
      </li>
      <li>
        <nuxt-link to="/">
          About
        </nuxt-link></li>
      <li>
        <nuxt-link to="/">
          Shop
        </nuxt-link>
      </li>
    </ul>
  </header>
</template>

<script>
import TjLogo from '../components/tjLogo'

export default {
  name: 'AppHeader',
  components: {
    TjLogo
  }
}
</script>

<style>
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 1rem;
}
.header ul {
}
</style>
