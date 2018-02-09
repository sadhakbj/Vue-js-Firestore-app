<template>
    <nav>
        <div class="nav-wrapper green">
            <div class="container">
                <router-link to="/" class="brand-logo">Employee Manager</router-link>
                <ul id="nav-mobile" class="right hide-on-med-and-down">
                    <li v-if="authUser">{{ authUser.email }}</a></li>
                    <li v-if="authUser"><a href="#" @click="logout">Log Out</a></li>
                </ul>
            </div>
        </div>
    </nav>
</template>
<script>
  /* eslint-disable indent */

  import firebase from 'firebase'

  export default {
    name: 'navBar',
    data() {
      return {
        authUser: ''
      }
    },
    created() {
      this.authUser = firebase.auth().currentUser
    },
    methods: {
      logout() {
        firebase.auth().signOut().then(() => {
            alert('Logged Out Successfully')
            this.authUser = ''
            this.$router.replace('login')
          }
          , error => {
            alert('Whoops something went wrong.')
          })
      }
    }
  }
</script>
