<template>
      <div class="mx-auto d-flex justify-center align-center" style="height: 95vh;">
        <v-card v-if="user" rounded="xl" width="390" class="pa-5" color="white">
          <v-card-text>
            <div class="d-flex align-centre ga-4" >
              <v-avatar size="70">
                <v-img :src="user.picture"/>
              </v-avatar>
              <div>
                <h2>{{ user.name }}</h2>
                <p>{{ user.email }}</p>
              </div>
            </div>
          </v-card-text>
          <v-card-actions>
            <v-btn  block color="pink" prepend-icon=mdi-logout class="d-flex mx-auto my-5 align-center justify-center" @click="logout">
              Logout
            </v-btn>
          </v-card-actions>
        </v-card>
      </div>  
</template>

<script setup lang="ts">
const user = ref<any>(null)

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