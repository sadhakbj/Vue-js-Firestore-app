<template>
    <div id="login">
        <div class="row">
            <br/> <h5>Register Quickly providing your email</h5>
            <div id="card-alert" class="card red lighten-5" v-if="message">
                <div class="card-content light-red-text">
                    <p style="color: red">{{ message }}</p>
                </div>
            </div>
            <form action="#" @submit.prevent="registerUser">
                <div class="row">
                    <div class="input-field col s12">
                        <input id="email" type="text" class="validate" placeholder="Email Address" required
                               v-model="email">
                    </div>
                </div>
                <div class="row">
                    <div class="input-field col s12">
                        <input id="password" type="password" class="validate" placeholder="Password" required
                               v-model="password">

                    </div>
                </div>
                <button class="btn green">Register</button>
                <router-link to="/" class="btn grey"><i class="fa fa-arrow-left"></i> Go back</router-link>
            </form>
        </div>
    </div>
</template>

<script>
  import firebase from 'firebase'

  export default {
    name: 'register',
    data() {
      return {
        email: '',
        password: '',
        message: ''
      }
    },
    methods: {
      registerUser() {
        firebase.auth().createUserWithEmailAndPassword(this.email, this.password)
          .then(user => this.$router.go({ path: this.$router.path }),
            error => {
              this.message = error.message
            }
          )
      }
    }
  }
</script>

<style>

</style>
