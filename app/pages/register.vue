<template>
  <div class="flex items-center justify-center min-h-screen bg-gray-50">
    <UCard class="w-full max-w-md mx-4">
      <template #header>
        <h2 class="text-xl font-semibold text-center">Create Account</h2>
      </template>

      <UForm @submit="handleRegister" :state="form" class="space-y-4">
        <UFormGroup label="First Name">
          <UInput v-model="form.firstName" placeholder="First Name" class="w-[90%] p-3 px-2" />
        </UFormGroup>

        <UFormGroup label="Last Name">
          <UInput v-model="form.lastName" placeholder="Last Name" class="w-[90%] p-3 px-2" />
        </UFormGroup>

        <UFormGroup label="Username">
          <UInput v-model="form.lastName" placeholder="Username" class="w-[90%] p-3 px-2" />
        </UFormGroup>

        <UFormGroup label="Email">
          <UInput v-model="form.email" type="email" placeholder="Email" class="w-[90%] p-3 px-2" />
        </UFormGroup>

        <UFormGroup label="Password">
          <UInput v-model="form.password" type="password" placeholder="Password" class="w-[90%] p-3 px-2" />
        </UFormGroup>

        <UFormGroup label="Confirm Password">
          <UInput v-model="form.password" type="password" placeholder="Confirm Password" class="w-[90%] p-3 px-2" />
        </UFormGroup>

        <UButton type="submit" color="primary" :loading="loading" class="w-full mt-4 justify-center items-center text-white">Register</UButton>
      </UForm>

      <p class="mt-4 text-sm text-center text-gray-500">
        Already have an account?
        <NuxtLink to="/" class="text-primary-600">Login</NuxtLink>
      </p>
    </UCard>
  </div>
</template>

<script setup>
definePageMeta({ layout: 'auth' })

// import { useAuth } from '~/composables/useAuth'
// const { register } = useAuth()
/**
 * DECLARATIONS
*/
  const form = reactive({
    name: '',
    email: '',
    password: ''
  })
  const loading = ref(false)

/**
 * CLICK HANDLER
*/
  const handleRegister = async (e) => {
    e.preventDefault()
    loading.value = true
    try {
      await register(form.name, form.email, form.password)
      navigateTo('/')
    } catch (err) {
      alert(err)
    } finally {
      loading.value = false
    }
  }
</script>
