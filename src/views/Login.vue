<template>
  <!--Login View -->
  <div id="login">
  <!--Toggle Password Reset -->
    <PasswordReset v-if="showPasswordReset" @close="togglePasswordReset()"></PasswordReset>
    <section>
        <!--App name and tagline -->
      <div class="col1">
        <h1>Build Early Ed</h1>
        <p>Welcome to Build Early Ed, the <a href="https://build-early-ed-webapp-h4lzp.ondigitalocean.app/" target="_blank">app </a> connecting New Mexicans to opportunities in Early Childhood Education</p>
      </div>
        <!--Login Section -->
      <div :class="{ 'signup-form': !showLoginForm }" class="col2">
        <form v-if="showLoginForm" @submit.prevent>
          <h1>Welcome Back</h1>
           <!--Insert Email -->
          <div>
            <label for="email1">Email</label>
            <input v-model.trim="loginForm.email" type="text" placeholder="you@email.com" id="email1" />
          </div>
           <!--Insert Password -->
          <div>
            <label for="password1">Password</label>
            <input v-model.trim="loginForm.password" type="password" placeholder="******" id="password1" />
          </div>
           <!--Allow users to click on Login, Password Reset, and Create an Account -->
          <button @click="login()" class="button">Log In</button>
          <div class="extras">
            <a @click="togglePasswordReset()">Forgot Password</a>
            <a @click="toggleForm()">Create an Account</a>
          </div>
        </form>
       <!--Create an Account Form -->
        <form v-else @submit.prevent>
          <h1>Get Started</h1>
          <!--Allow users to input their name, include placeholder text -->
          <div>
            <label for="name">Name</label>
            <input v-model.trim="signupForm.name" type="text" placeholder="Early Ed Trailblazer" id="name" />
          </div>
          <!--Allow users to input their title, include placeholder text -->
          <div>
            <label for="title">Title</label>
            <input v-model.trim="signupForm.title" type="text" placeholder="Company" id="title" />
          </div>
          <!--Allow users to insert their email-->
          <div>
            <label for="email2">Email</label>
            <input v-model.trim="signupForm.email" type="text" placeholder="you@email.com" id="email2" />
          </div>
          <div>
          <!--Allow users to insert their password-->
            <label for="password2">Password</label>
            <input v-model.trim="signupForm.password" type="password" placeholder="min 6 characters" id="password2" />
          </div>
          <!--Sign Up Button-->
          <button @click="signup()" class="button">Sign Up</button>
          <!--Back to log in action-->
          <div class="extras">
            <a @click="toggleForm()">Back to Log In</a>
          </div>
        </form>
      </div>
    </section>
  </div>
</template>

<!--To expand on the log in features, create dual log-in portals for community members and organizations to customize features and user privileges for different users as they interact with the site. To strengthen security for users, leverage Firebase security rules to build user-based and role-based access systems to ensure the safety of users' data, whether user is a community organization or individual. Use authentication rules to confirm the identify of users requesting access to Build Early Ed data. Include user information in rules to control access to data based on user identity. Ensure users can only read and write their own data in requests. -->

<script>
import PasswordReset from '@/components/PasswordReset'

export default {
  components: {
    PasswordReset
  },
  data() {
    return {
      loginForm: {
        email: '',
        password: ''
      },
      signupForm: {
        name: '',
        title: '',
        email: '',
        password: ''
      },
      showLoginForm: true,
      showPasswordReset: false
    }
  },
  methods: {
//create a method for login form
    toggleForm() {
      this.showLoginForm = !this.showLoginForm
    },
    // create a method for users to reset password
    togglePasswordReset() {
      this.showPasswordReset = !this.showPasswordReset
    },
    //create a method for users to login
    login() {
      this.$store.dispatch('login', {
        email: this.loginForm.email,
        password: this.loginForm.password
      })
    },
    //create a method for users to sign up
    signup() {
      this.$store.dispatch('signup', {
        email: this.signupForm.email,
        password: this.signupForm.password,
        name: this.signupForm.name,
        title: this.signupForm.title
      })
    }
  }
}
</script>
