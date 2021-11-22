<template>
  <section class="authentication">
    <div class="auth-body">
      <h1 class="text-uppercase fw-500 mb-4 text-center font-22">
        Reset Password
      </h1>
      <form class="auth-form" @submit.prevent="submit">
        <AlertSuccess :form="form">{{ status }}</AlertSuccess>
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
        <div class="text-right">
          <button :disabled="form.busy" type="submit" class="btn btn-primary primary-bg-color font-16 fw-500 text-uppercase">
            <span v-if="form.busy"><i class="fas fa-spinner fa-spin"></i></span>
            Send Reset Link
          </button>
        </div>
        <p class="font-14 fw-400 text-center mt-4">
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
        email: ''
      }),
      status: ''
    };
  },

  methods: {
    submit() {
      this.form.post('/password/email').then(resp => {
        this.status = resp.data.status;
      }).catch(error => {
        console.log(error);
      });
    }
  }
};
</script>
