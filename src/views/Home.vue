<template>
  <v-container>
    <p v-for="cpu in allCPU" :key="cpu.model">
      {{ cpu.brand }} | {{ cpu.model }} | {{ cpu.cores }} Cores ({{
        cpu.threads
      }}
      Threads)
    </p>
  </v-container>
</template>

<script>
import { gql } from "graphql-tag";

export default {
  name: "Home",

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
