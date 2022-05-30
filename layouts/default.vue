<template>
  <v-app dark>
    <v-main>
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>
    <v-footer
      dark
      padless
    >
      <v-card
        class="flex"
        flat
        tile
      >
        <v-card-text class="py-2 white--text text-center teal">
          {{ new Date().getFullYear() }} — <strong>Martín Lejman</strong>
          <v-btn
            class="mx-4"
            dark
            icon
            href="https://github.com/marezelej"
            target="_blank"
          >
            <v-icon size="24px">mdi-github</v-icon>
          </v-btn>
        </v-card-text>
      </v-card>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  name: 'DefaultLayout',
}
</script>
