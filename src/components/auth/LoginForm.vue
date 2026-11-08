<template>
  <div class="q-pa-md q-gutter-y-md" style="max-width: 400px">
    <h3>Login</h3>
    <q-input filled v-model="email" label="Your email *" />

    <q-input filled type="password" v-model="password" label="Your password *" />
    <div>
      <q-btn @click="signin" label="Send" type="button" color="primary" />
      <q-btn label="Reset" type="reset" color="primary" flat class="q-ml-sm" />
    </div>
  </div>
</template>

<style scoped></style>

<script setup>
import { useQuasar } from 'quasar'
import { ref } from 'vue'
import axios from 'axios'

const $q = useQuasar()

const email = ref(null)
const password = ref(null)

function signin() {
  let url = 'http://localhost:5208/api/users/signin'
  let data = {
    email: email.value,
    password: password.value,
  }

  axios
    .post(url, data)
    .then((response) => {
      console.log(response.data)
      $q.notify({
        type: 'positive',
        message: 'Login successful!',
      })
    })
    .catch((error) => {
      console.error(error)
      $q.notify({
        type: 'negative',
        message: 'Login failed. Please check your credentials.',
      })
    })
}
</script>
