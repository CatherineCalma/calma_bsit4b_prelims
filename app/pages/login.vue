<template>
  <div class="d-flex mx-auto align-center justify-center" style="height: 90vh">
    <v-card width="500" rounded="xl" color="white">
      <v-card-text class="text-center" mx-8 my-5>
        <v-icon size="150" color="pink">mdi-account</v-icon>
        <p class="my-3" >Welcome back! please sign in</p>
        <v-form>
          <v-text-field label="Username or Email" variant="outlined" ></v-text-field>
          <v-text-field label="Password" type="password" variant="outlined" ></v-text-field>
        </v-form>

        <v-btn color="pink" block>Sign in</v-btn>
        <v-divider class="my-5">OR</v-divider>
        <v-btn color="black" prependIcon="mdi-google" block @click="loginWithGoogle">Sign in with Google</v-btn>

      </v-card-text>
    </v-card>
  </div>
</template>

<script lang="ts" setup>
//@ts-nocheck
const config =useRuntimeConfig()
declare global {
  interface Window {
    google: any
  }
}

//loginWithGoogle Function
const loginWithGoogle = () => {
  const client = window.google.accounts.oauth2.initTokenClient({
    client_id: config.public.googleClientId,
    scope: "openid email profile",
    callback: async (response: any) => {
      const userInfo =await $fetch(
        "https://www.googleapis.com/oauth2/v3/userinfo",
        {
          headers: {
            Authorization: `Bearer ${response.access_token}`,
          },
        },
      );

      localStorage.setItem("google_user", JSON.stringify(userInfo));
      localStorage.setItem("google_token", response.access_token);

      navigateTo("/");
    },
  });

  client.requestAccessToken();
};

</script>

<style>

</style>