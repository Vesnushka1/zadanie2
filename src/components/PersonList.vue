<template>
  <one-person @openDialogValue="this.$emit('openDialogValue', true, person)" v-for="person in persons" :key="person.id" :person="person"></one-person>
</template>

<script>
import OnePerson from "@/components/OnePerson";
export default {
  components: {OnePerson},
  props: {
    persons: {
      type: Array
    }
  }
}
</script>

<style scoped>

</style>