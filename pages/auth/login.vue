<template>
  <section class="authentication">
    <div class="auth-body">
      <h1 class="text-uppercase fw-500 mb-4 text-center font-22">
        Login
      </h1>
      <form class="auth-form" @submit.prevent="submit">
        <AlertError v-if="form.errors.has('message')" :form="form">
          {{ form.errors.get('message') }}
          <nuxt-link :to="{name: 'verification.resend'}">Resend verification email</nuxt-link>
        </AlertError>
        <div class="form-group">
          <input
            v-model.trim="form.email"
            type="text"
            name="email"
            class="form-control form-control-lg font-14 fw-300"
            :class="{'is-invalid': form.errors.has('email')}"
            placeholder="Email"
          />
          <HasError :form="form" field="email" />
        </div>
        <div class="form-group">
          <input
            v-model.trim="form.password"
            type="password"
            name="password"
            class="form-control form-control-lg font-14 fw-300"
            :class="{'is-invalid': form.errors.has('password')}"
            placeholder="Password"
          />
          <HasError :form="form" field="password" />
        </div>
        <div class="mt-4 mb-4 clearfix">
          <nuxt-link :to="{name: 'password.email'}" class="forgot-pass color-blue font-14 fw-400" href="#"> Forgot password? </nuxt-link>
        </div>
        <div class="text-right">
          <button :disabled="form.busy" type="submit" class="btn btn-primary primary-bg-color font-16 fw-500 text-uppercase">
            <span v-if="form.busy"><i class="fas fa-spinner fa-spin"></i></span>
            Login
          </button>
        </div>
        <p class="font-14 fw-400 text-center mt-4">
          Don't have an account yet?
          <nuxt-link :to="{name: 'register'}" class="color-blue"> Create an account</nuxt-link>
        </p>
      </form>
    </div>
  </section>
</template>

<script>
export default {
  data() {
    return {
      form: this.$vform({
        email: '',
        password: ''
      })
    };
  },

  methods: {
    submit() {
      this.$auth.loginWith('local', {
        data: this.form.data()
      }).then(resp => {
        console.log(resp);
      }).catch(err => {
        this.form.errors.set(err.response.data);
      });
    }
  }
};
</script>
