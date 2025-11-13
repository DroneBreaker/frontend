<template>
  <div class="flex items-center justify-center min-h-screen bg-gray-50">
    <UCard class="w-full max-w-md mx-4">
      <template #header>
        <h2 class="text-xl font-semibold text-center">Login</h2>
      </template>

      <UForm @submit="handleLogin" :state="form" class="items-center">
        <UFormGroup label="TIN" class="mx-4">
          <UInput v-model="form.tin" type="text" placeholder="Business TIN" class="w-[90%] p-3 px-2" />
        </UFormGroup>

        <UFormGroup label="Username" class="mx-4">
          <UInput v-model="form.username" type="text" placeholder="Username" class="w-[90%] p-3 px-2" />
        </UFormGroup>

        <UFormGroup label="Email" class="mx-4">
          <UInput v-model="form.email" type="email" placeholder="Email" class="w-[90%] p-3 px-2" />
        </UFormGroup>

        <UFormGroup label="Password" class="mx-4">
          <UInput v-model="form.password" type="password" placeholder="Password" class="w-[90%] p-3 px-2" />
        </UFormGroup>

        <UContainer>
          <UButton type="submit" color="primary" :loading="loading" class="w-full mt-4 justify-center items-center text-white">Login</UButton>
        </UContainer>
      </UForm>

      <p class="mt-4 text-sm text-center text-gray-500">
        Don’t have an account?
        <NuxtLink to="/register" class="text-primary-600">Register</NuxtLink>
      </p>
    </UCard>
  </div>
</template>

<script setup>
definePageMeta({ layout: 'auth' })

/**
 * IMPORTS
*/
  // import { useAuth } from '~/composables/useAuth'

/**
 * DECLARATIONS
*/
  // const { login } = useAuth()

  const form = reactive({
    business_tin: '',
    username: '',
    email: '',
    password: ''
  })
  const loading = ref(false)

/**
  * CLICK HANDLERS
*/
  const handleLogin = async (e) => {
    e.preventDefault()
    loading.value = true
    try {
        await login(form.business_tin, form.username, form.email, form.password)
        navigateTo('/dashboard')
    } catch (err) {
        alert(err)
    } finally {
        loading.value = false
    }
  }
</script>
