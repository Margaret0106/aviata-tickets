<template>
  <div class="tickets__list tickets-list">    
    <template v-if="flights.length > 0">
      <ticket
        v-for="flight in flights"
        v-bind:key="flight.id"
        v-bind:flight="flight"
        class="tickets-list__item">
      </ticket>  
    </template>
    <template v-else>
      <p class="not-found">Рейсов не найдено :(</p>
    </template>    
  </div>
</template>      


<script>
  import Ticket from './Ticket.vue'

  export default {
    name: 'tickets-list',
    props: ['flights'],    
    components: {
      Ticket
    }
  }
</script>

<style lang="scss" src="../assets/styles/tickets.scss"/>
