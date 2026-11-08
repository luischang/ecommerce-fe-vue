<template>
  <q-form
    class="q-pa-md q-gutter-y-md"
    style="width: 100%; max-width: 400px"
    @submit.prevent="register"
  >
    <h3>Register</h3>

    <q-input v-model="firstName" filled label="First name *" :rules="[requiredRule]" />
    <q-input v-model="lastName" filled label="Last name *" :rules="[requiredRule]" />
    <q-input
      v-model="dateOfBirth"
      filled
      type="date"
      label="Date of birth *"
      :rules="[requiredRule]"
    />
    <q-input v-model="country" filled label="Country *" :rules="[requiredRule]" />
    <q-input v-model="address" filled label="Address *" :rules="[requiredRule]" />
    <q-input v-model="email" filled type="email" label="Email *" :rules="[requiredRule]" />
    <q-input v-model="password" filled type="password" label="Password *" :rules="[requiredRule]" />

    <div class="q-gutter-x-sm">
      <q-btn label="Register" type="submit" color="primary" :loading="isSubmitting" />
      <q-btn label="Reset" type="reset" color="primary" flat @click="resetForm" />
    </div>
  </q-form>
</template>

<script setup>
import axios from 'axios'
import { useQuasar } from 'quasar'
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const $q = useQuasar()
const router = useRouter()

const firstName = ref('')
const lastName = ref('')
const dateOfBirth = ref('')
const country = ref('')
const address = ref('')
const email = ref('')
const password = ref('')
const isSubmitting = ref(false)

const requiredRule = (value) => Boolean(value) || 'This field is required'

function resetForm() {
  firstName.value = ''
  lastName.value = ''
  dateOfBirth.value = ''
  country.value = ''
  address.value = ''
  email.value = ''
  password.value = ''
}

async function register() {
  isSubmitting.value = true

  try {
    await axios.post('http://localhost:5208/api/users/signup', {
      firstName: firstName.value,
      lastName: lastName.value,
      dateOfBirth: dateOfBirth.value,
      country: country.value,
      address: address.value,
      email: email.value,
      password: password.value,
    })

    $q.notify({
      type: 'positive',
      message: 'Registration successful!',
    })
    await router.push('/login')
  } catch (error) {
    console.error(error)
    $q.notify({
      type: 'negative',
      message: 'Registration failed. Please try again.',
    })
  } finally {
    isSubmitting.value = false
  }
}
</script>
