<template>
  <v-app id="inspire">

    <v-navigation-drawer v-model="drawer">
      <v-list>
        <v-list-item>
          <v-list-item-title>Menu</v-list-item-title>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar>
      <v-app-bar-nav-icon
        @click="drawer = !drawer"
      ></v-app-bar-nav-icon>

      <v-app-bar-title>
        System Integration
      </v-app-bar-title>
    </v-app-bar>

    <v-main>
      <v-container>
        <v-card v-if="user" class="pa-6"
        >
          <div class="d-flex align-center ga-4">
            <v-avatar size="64">
              <v-img :src="user.picture"></v-img>
            </v-avatar>

            <div>
              <h2>{{ user.name }}</h2>
              <p>{{ user.email }}</p>
            </div>

          </div>
        </v-card>

        <v-btn
          class="d-flex mx-auto my-5" color="pink" @click="logout">Logout</v-btn>

      </v-container>
    </v-main>

  </v-app>
</template>


<script setup lang="ts">

import { ref, onMounted } from 'vue'

const user = ref<any>(null)
const drawer = ref(false)

onMounted(() => {

  const savedUser = localStorage.getItem('google_user')

  if (savedUser) {
    user.value = JSON.parse(savedUser)
  }

})

const logout = () => {
  localStorage.removeItem('google_user')
  localStorage.removeItem('google_token')
  navigateTo('/login')
}
</script>