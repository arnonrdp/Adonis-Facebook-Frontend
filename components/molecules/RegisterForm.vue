<template>
  <form @submit.prevent="onSubmit">
    <div class="fom-field">
      <BaseInput v-model="email" type="email" placeholder="E-mail" />
    </div>

    <BaseButton text="Próxima etapa" />
  </form>
</template>

<script lang="ts">
import Vue from 'vue'
import { userRegister } from '@/store'

export default Vue.extend({
  data() {
    return {
      email: ''
    }
  },
  methods: {
    async onSubmit() {
      try {
        await userRegister.create({
          email: this.email,
          redirectUrl: 'https://arnon-facebook.vercel.app/register'
        })

        this.email = ''

        this.$notify({ type: 'success', text: 'E-mail enviado com sucesso' })
      } catch {
        this.$notify({ type: 'error', text: 'Erro ao enviar e-mail' })
      }
    }
  }
})
</script>

<style lang="scss" scoped>
form {
  display: grid;
  grid-gap: 0.8rem;

  button {
    width: 100%;
  }

  a {
    justify-self: end;
    font-size: 14px;
    color: color(white);
  }

  input {
    width: 100% !important;
    padding: 0.7rem 1.2rem;
  }
}
</style>
