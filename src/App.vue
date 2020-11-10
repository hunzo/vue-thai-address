<template>
  <v-app>
    <v-main>
      <AddressEng/>
      <AddressThai/>
    </v-main>
  </v-app>
</template>

<script>
import AddressEng from './components/AddressEng'
import AddressThai from './components/AddressThai'

export default {
  name: 'App',

  components: {
    AddressEng,
    AddressThai
  },

  data: () => ({
    //
  }),
};
</script>
