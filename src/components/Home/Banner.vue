<template>
  <div>
    <div class="bg-accent">
      <v-row class="justify-center">
        <span
          class="
            mt-8
            text-h5 text-sm-h4 text-md-h3 text-lg-h2
            white--text
            font-weight-bold
          "
          :class="{
            'mb-8': !$vuetify.breakpoint.smAndDown,
            'mb-0': $vuetify.breakpoint.smAndDown,
          }"
        >
          Open Source PC Parts API
        </span>
      </v-row>
      <v-row
        class="justify-center"
        :class="{
          'mt-16': !$vuetify.breakpoint.smAndDown,
          'mt-8': $vuetify.breakpoint.smAndDown,
          'pb-8': $vuetify.breakpoint.smAndDown,
        }"
      >
        <v-btn
          outlined
          rounded
          color="white"
          :class="{
            'mr-2': $vuetify.breakpoint.smAndDown,
            'mr-6': !$vuetify.breakpoint.smAndDown,
          }"
        >
          <v-icon class="mr-2">mdi-github</v-icon>
          <span>
            {{ $vuetify.breakpoint.smAndDown ? "API" : "API Github" }}
          </span>
        </v-btn>
        <v-btn outlined rounded color="white">
          <v-icon class="mr-2">mdi-github</v-icon>
          <span>
            {{ $vuetify.breakpoint.smAndDown ? "Website" : "Website Github" }}
          </span>
        </v-btn>
      </v-row>
    </div>
    <div>
      <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 80 1440 150">
        <path
          fill="var(--v-accent-base)"
          fill-opacity="1"
          d="M0,128L48,149.3C96,171,192,213,288,213.3C384,213,480,171,576,165.3C672,160,768,192,864,192C960,192,1056,160,1152,144C1248,128,1344,128,1392,128L1440,128L1440,0L1392,0C1344,0,1248,0,1152,0C1056,0,960,0,864,0C768,0,672,0,576,0C480,0,384,0,288,0C192,0,96,0,48,0L0,0Z"
          data-darkreader-inline-fill=""
          style="--darkreader-inline-fill: var(--v-accent-base)"
        ></path>
      </svg>
    </div>
  </div>
</template>

<script>
export default {};
</script>

<style>
</style>