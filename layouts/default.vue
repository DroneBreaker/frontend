<template>
  <div class="flex min-h-screen bg-gray-50">
    <!-- Sidebar -->
    <aside class="w-64 bg-white border-r border-gray-200 flex flex-col justify-between">
      <div>
        <div class="p-4 text-2xl font-bold text-primary-600">
          POS App
        </div>

        <nav class="mt-4 space-y-1">
          <NuxtLink
            v-for="link in links"
            :key="link.to"
            :to="link.to"
            class="block px-4 py-2 rounded-md hover:bg-gray-100 transition"
            :class="{ 'bg-gray-100 font-semibold text-primary-700': route.path === link.to }"
          >
            {{ link.label }}
          </NuxtLink>
        </nav>
      </div>

      <div class="p-4">
        <UButton color="gray" block @click="logoutUser">Logout</UButton>
      </div>
    </aside>

    <!-- Main content -->
    <main class="flex-1 p-6">
      <slot />
    </main>
  </div>
</template>

<script setup>
import { useAuth } from '~/composables/useAuth'
const { logout } = useAuth()
const route = useRoute()

const links = [
  { label: 'Dashboard', to: '/' },
  { label: 'Sales', to: '/sales' },
  { label: 'Inventory', to: '/inventory' },
  { label: 'Reports', to: '/reports' }
]

const logoutUser = () => {
  logout()
  navigateTo('/auth/login')
}
</script>

<style scoped>
/* Optional shadow or style */
aside {
  box-shadow: 0 0 8px rgba(0, 0, 0, 0.04);
}
</style>
