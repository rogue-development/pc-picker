<template>
  <v-container fluid class="px-0">
    <Banner />
    <v-container>
      <p v-for="cpu in allCPU" :key="cpu.model">
        {{ cpu.brand }} | {{ cpu.model }} | {{ cpu.cores }} Cores ({{
          cpu.threads
        }}
        Threads)
      </p>
    </v-container>
  </v-container>
</template>

<script>
import { gql } from "graphql-tag";
import Banner from "../components/Home/Banner.vue";

export default {
  name: "Home",

  components: {
    Banner,
  },

  apollo: {
    allCPU: gql`
      query getAllCPUs {
        allCPU {
          brand
          model
          cores
          threads
        }
      }
    `,
  },
};
</script>
