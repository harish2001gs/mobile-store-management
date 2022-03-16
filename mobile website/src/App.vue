<template>
  <div id="wrapper">
    <nav class="navbar is-light">
      <div class="navabar-brand">
        <router-link to="/" class="navbar-item"><strong>Apple Mobiles</strong></router-link>
        <a class="navbar-burger" aria-label="menu" aria-expanded="false" data-target="navbar-menu" @click="showMobileMenu = !showMobileMenu">
          <span aria-hidden="true"></span>
          <span aria-hidden="true"></span>
          <span aria-hidden="true"></span>
        </a>
        </div>

    <div class="navbar-menu" id="navbar-menu" v-bind:class="{'is-active':showMobileMenu}">
      <div class="navbar-end">
        <router-link to="/mobilephones" class="navbar-item">Mobile Phones</router-link>
        <router-link to="/tablet" class="navbar-item">Tablets</router-link>

        <div class="navbar-item">
            <div class="buttons">
              <template v-if="$store.state.isAuthenticated">
                <router-link to="/my-account" class="button is-light">My account</router-link>
              </template>

        <template v-else>
                <router-link to="/log-in" class="button is-light">Log in</router-link>
        </template>

        <div class="navbar-items">
          <div class="buttons">
            <router-link to="/cart" class="button is-success">
            <span class="icon"><i class="fas fa-shopping-cart"></i></span>
            <span>Cart ({{cartToLength}})</span>
            </router-link>
            </div>
            </div>
            </div>
        </div>
    </div>
    </div>
    </nav>
    <section class="section">
      <router-view/>
    </section>

    <footer class="footer">
      <p class="has-text-centered">Copyright @c 2021 </p>
    </footer>
  </div>
</template>

<script>
import axios from 'axios'
export default{
  data(){
    return {
      showMobileMenu : false,
      cart: {
        items: []
      }
    }  
  },
  beforeCreate()
  {
    this.$store.commit('initializeStore')
    const token = this.$store.state.token
    if (token) {
        axios.defaults.headers.common['Authorization'] = "Token " + token
    } else {
        axios.defaults.headers.common['Authorization'] = ""
    }
  },
  mounted()
  {
    this.cart = this.$store.state.cart
  },
  computed:{
    cartToLength()
    {
      let totalength = 0
      for(let i =0 ; i<this.cart.items.length;i++)
      {
        totalength += this.cart.items[i].quantity
      }
      return totalength
    }
  }
}
</script>

<style lang="scss">
@import '../../node_modules/bulma';
</style>
