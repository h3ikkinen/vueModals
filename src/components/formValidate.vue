<template>
    <modal
      v-bind:title="title"
      @close="onClose"
      >
    <template v-slot:body>
        <form @submit.prevent="onSubmit">
            <div class="form-item" :class="{ errorInput: $v.email.$error }">
              <label for="#LoginName">Login </label>
              <input
                  id="LoginName"
                  v-model="email"
                  :class="{ errorInput: $v.email.$error }"
                  @change="$v.email.$touch()"
              />
              <p class="errorText" :class="{errorTextActive: !$v.email.required}">
                Field is required!
              </p>
              <p class="errorText" :class="{errorTextActive: !$v.email.email}">
                Email with not correct!
              </p>    
            </div>
            <div class="form-item" :class="{ errorInput: $v.password.$error }">
              <label class="form__label">Password</label>
              <input type="password" class="form__input" v-model.trim="$v.password.$model" />
              <p class="errorText" :class="{errorTextActive: !$v.password.required}">
                Field is required!
              </p>
              <p class="errorText" :class="{errorTextActive: !$v.password.minLength}">
                Name must have at least {{ $v.password.$params.minLength.min }} !
              </p>    
            </div>
            <button class="btn">
              Login
            </button>
        </form>
    </template>
  </modal>
</template>

<script>
import { required, email, minLength  } from 'vuelidate/lib/validators';
import modal from "@/components/UI/modal.vue";
export default {
  data() {
    return {
      password: '',
      email: '',
    };
  },
  props: {
    title: {
      type: String,
      required: true
    }
  },
  validations: {
    email: {
      required,
      email,
    },
    password: {
      required,
      minLength: minLength(6)
    },
  },
  components: {
    modal,
  },
  methods: {
    onSubmit () {
      this.$v.$touch();
      if (!this.$v.$invalid) {
        const user = {
          email: this.email,
          pass: this.password,
        }
        console.log(user)
        this.password = ''
        this.email = ''
        this.$v.$reset()
        this.$emit('close')
      }
    },
    onClose () {
      this.password = '';
      this.$v.$reset();
      this.$emit('close')
    }
  },
};
</script>

<style lang="scss">
  .form-item {
    .errorText {
      visibility: hidden;
      opacity: 0;
      font-size: 15px;
      margin-top: 25px;
      color: #b42f2f;
      transform: translateY(-100%);
      transition: .2s;
      position: absolute;
      bottom: 0;
      left: 0;
    }
    &.errorInput .errorText {
      &.errorTextActive {
        visibility: visible;
        opacity: 1;
        z-index: inherit;
        transform: translateY(0);
      }
    }

  }
  input.errorInput {
    border-color: #b42f2f;
  }
</style>