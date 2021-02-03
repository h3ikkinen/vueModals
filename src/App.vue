<template>
  <div id="app">
    <div class="container"> 
      <button @click="modalLogin.show = !modalLogin.show" class="btn">Login</button>
      <formValidate 
        v-bind:title="modalLogin.title" 
        @close="modalLogin.show = false" 
        v-show="modalLogin.show" />
      <button @click="modalReg.show = !modalReg.show" class="btn">Registration</button>
      <reg 
        v-bind:title="modalReg.title" 
        @close="modalReg.show = false" 
        v-show="modalReg.show" />
    </div>
  </div>
</template>

<script>
  import formValidate from '@/components/formValidate.vue';
  import reg from '@/components/Registration.vue';
  export default {
    data () {
      return({
        modalLogin: {
          title: 'Login',
          show: false,
        },
        modalReg: {
          title: 'Registration',
          show: false,
          inputName: '',
          inputTel: '',
        },
      })
    },
    components: {
        formValidate, reg
    },
    methods: {
    }
  }
</script>

<style>

</style>
