<template>
<!-- Section Cards -->
  <section class="authentication">
    <div class="auth-body">
      <h1 class="text-uppercase fw-500 mb-4 text-center font-22">
        Register
      </h1>
      <form class="auth-form" @submit.prevent="submit">
        <AlertSuccess :form="form">We have sent you and email to active you account</AlertSuccess>
        <div class="form-group">
          <input
            v-model.trim="form.name"
            type="text"
            name="name"
            class="form-control form-control-lg font-14 fw-300"
            :class="{'is-invalid': form.errors.has('name')}"
            placeholder="Full Name"
          />
          <HasError :form="form" field="name" />
        </div>
        <div class="form-group">
          <input
            v-model.trim="form.username"
            name="username"
            class="form-control form-control-lg font-14 fw-300"
            :class="{'is-invalid': form.errors.has('username')}"
            placeholder="Username"
          />
          <HasError :form="form" field="username" />
        </div>
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
        <div class="form-group">
          <input
            v-model.trim="form.password_confirmation"
            type="password"
            name="password_confirmation"
            class="form-control form-control-lg font-14 fw-300"
            :class="{'is-invalid': form.errors.has('password_confirmation')}"
            placeholder="Confirm Password"
          />
          <HasError :form="form" field="password_confirmation" />
        </div>

        <div class="text-right">
          <button :disabled="form.busy" type="submit" class="btn btn-primary primary-bg-color font-16 fw-500 text-uppercase">
            <span v-if="form.busy"><i class="fas fa-spinner fa-spin"></i></span>
            Register
          </button>
        </div>
        <p class="font-14 fw-400 text-center mt-4">
          Already have an account?
          <nuxt-link :to="{name: 'login'}" class="color-blue"> Login</nuxt-link>
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
         username: '',
         name: '',
         email: '',
         password: '',
         password_confirmation: ''
       })
     };
  },

  methods: {
    submit() {
      this.form.post('/register').then((resp) => {
        this.form.reset();
      }).catch((err) => {
        console.log(err);
      });
    }
  }
};
</script>
