<template>
  <div class="row">
    <div class="col-lg-6 offset-lg-3">
      <div class="card text-black bg-light">
        <div class="card-body">
          <form @submit.prevent="submit">
            <h2>Sign In</h2>
            <p>Please provide required information to continue.</p>

            <div class="form-group">
              <label>Username</label>
              <input class="form-control"
                     type="text"
                     autocomplete="username"
                     placeholder="Username"
                     name="username"
                     v-model="form.model.username"
                     v-validate="'required|min:3|max:16'">
              <span class="invalid-feedback"
                    v-show="errors.has('username')"
                    v-html="errors.first('username')" />
            </div>

            <div class="form-group">
              <label>Password</label>
              <input class="form-control"
                     type="password"
                     autocomplete="new-password"
                     placeholder="Password"
                     name="password"
                     v-model="form.model.password"
                     v-validate="'required|min:6|max:16'">
              <span class="invalid-feedback"
                    v-show="errors.has('password')"
                    v-html="errors.first('password')" />
            </div>

            <button class="btn btn-dark btn-block"
                    type="submit"
                    :disabled="errors.any()">
              <span class="fi fi-key" /> Sign In
            </button>

            <br>

            <router-link class="btn-link"
                         to="/auth/register">
              Don't have an account?
            </router-link>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { mapActions } from 'vuex'

export default {
  data() {
    return {
      form: {
        model: {
          password: 'tim-password',
          username: 'tim'
        }
      }
    }
  },

  methods: {
    ...mapActions(['login']),

    submit() {
      this.$validator.validateAll().then(res => {
        if (res) {
          this.login(this.form.model)
        } else {
          swal(
            'Not so fast!',
            'Please provide required data in valid format',
            'warning'
          )
        }
      })
    }
  }
}
</script>

<style lang='stylus'>
</style>
