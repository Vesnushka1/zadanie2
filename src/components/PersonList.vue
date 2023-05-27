<template>
  <one-person :successfulAuth="successfulAuth"
              @favPersonDel="this.$emit('favPersonDel', person)"
              @favPerson="this.$emit('favPerson', person)"
              @openDialogValue="this.$emit('openDialogValue', true, person)"
              v-for="person in persons" :key="person.id" :person="person"></one-person>
</template>

<script>
import OnePerson from "@/components/OnePerson";

export default {
  components: {OnePerson},
  props: {
    persons: {
      type: Array
    },
    successfulAuth: {
      type: Boolean
    }
  }
}
</script>

<style scoped>

</style>