<template>
  <div id="app">
    <div class="container">
      <div class="tickets">
        <tickets-filters :airlines="airlines" />
        <tickets-list :flights="flights" :airlines="airlines" />
      </div>
    </div>
  </div>
</template>

<script>
  import TicketsList from './components/TicketsList.vue'
  import TicketsFilters from './components/TicketsFilters.vue'

  export default {
    name: 'app',
    data() {
      return {
        airlines: {}, 
        flights: {}
      };
    },
    created() {
      this.getData();
    },
    methods: {
      getData() {
        fetch('results.json')
          .then(response => response.json())
          .then(data => {
            return (
              this.airlines = data.airlines,
              this.flights = data.flights
            )
          });
      }
    },
    components: {
      TicketsList,
      TicketsFilters
    }
  }
</script>


<style lang="scss">
  @import 'assets/styles/layout.scss';
  @import 'normalize-scss';
  @include normalize();
</style>