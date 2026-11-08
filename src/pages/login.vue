<template>
  <q-layout class="q-gutter-md">
    <q-page-container class="flex flex-center">
      <q-page class="row items-center justify-evenly">
        <LoginForm />
      </q-page>
    </q-page-container>
  </q-layout>
</template>

<script setup>
import LoginForm from '@/components/auth/LoginForm.vue'
</script>
