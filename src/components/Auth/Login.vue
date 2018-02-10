<template>
    <div id="login">
        <div class="row">
            <form action="#" method="post" @submit.prevent="processLogin">
                <div class="row">
                    <div class="input-field col s12">
                        <input id="email" type="text" class="validate" placeholder="Email" required
                               v-model="email">

                    </div>
                </div>
                <div class="row">
                    <div class="input-field col s12">
                        <input id="password" type="password" class="validate" placeholder="Password" required
                               v-model="password">

                    </div>
                </div>
                <button class="btn green"><i class="fa fa-sign-in"></i> Login</button>
                <router-link to="/register" class="btn blue"><i class="fa fa-user"></i> Create a account</router-link>
            </form>
        </div>
    </div>
</template>

<script>
  import firebase from 'firebase'

  export default {
    name: "login",
    data() {
      return {
        posts: [],
        email: '',
        password: ''
      }
    },
    methods: {
      processLogin() {
        firebase.auth().signInWithEmailAndPassword(this.email, this.password)
          .then(user => {
            this.$router.replace('admin')
            location.reload()
            this.$router.go({ path: this.$router.path })
          }, error => alert('Unable to login' + error.message))
      }
    }
  };
</script>

<style>

</style>
