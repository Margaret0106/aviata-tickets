<template>
  <div class="tickets__list tickets-list">    
    <ticket 
      v-for="flight in flights"
      v-bind:key="flight.id"
      v-bind:flight="flight"
      v-bind:airlines="airlines">
    </ticket>  
  </div>
</template>      


<script>
  import Ticket from './Ticket.vue'

  export default {
    name: 'tickets-list',
    props: ['flights', 'airlines'],    
    components: {
      Ticket
    }
  }
</script>

<style lang="scss" src="../assets/styles/tickets.scss"/>
