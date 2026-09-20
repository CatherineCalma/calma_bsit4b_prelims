<template>
  <v-card>
    <v-layout>
      <v-navigation-drawer v-model="drawer" theme="light">
        <v-list>
          <v-list-item
            prepend-avatar="https://i.pinimg.com/originals/83/b0/7f/83b07fe79c4bdcc8e6c27f974c597842.jpg?nii=t"
            subtitle="cath@gmailcom"
            title="Catherine Calma"
          ></v-list-item>
        </v-list>

        <v-divider></v-divider>

        <v-list density="compact" nav>
          <v-list-item prepend-icon="mdi-view-dashboard" title="Dashboard" to="/"></v-list-item>
          <v-list-item prepend-icon="mdi-qrcode" title="QR Code" to="/qr-code"></v-list-item>
          <v-list-item prepend-icon="mdi-weather-cloudy" title="Weather App" to="/weather"></v-list-item>
        </v-list>
      </v-navigation-drawer>

      <v-app-bar>
        <template v-slot:prepend>
          <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
        </template>

         <v-app-bar-title>Application Bar</v-app-bar-title>
      </v-app-bar>

      <v-main>
        <v-container fluid>
          <slot/>
        </v-container>
      </v-main>

    </v-layout>
  </v-card>
</template>

<script setup>
const drawer = ref(true)
</script>