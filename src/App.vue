<template>
  <div id="app">
    <div class="container">
      <div class="tickets">
        <tickets-filters :airlines="airlines" :active="activeFilters" @filter="filter" />
        <tickets-list :flights="filteredFlights"/>
        <div v-if="activeFilters" class="overlay" @click="toggleFilters"></div>
        <button v-if="activeFilters" class="btn btn--round btn--orange close-filters" @click="toggleFilters"></button>
        <button v-if="!activeFilters" class="btn btn--orange show-filters" @click="toggleFilters">Показать фильтры</button>
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
        flights: {},
        filteredFlights: {},
        activeFilters: false
      };
    },
    created() {
      this.getData();
    },
    watch: {
      flights: function() {
        this.filteredFlights = this.flights;
      }      
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
      },    
      filterByCarrier(codes, flight) {         
        if(codes.length === 0) {
          return true
        }     
        return codes.includes(flight.validating_carrier)      
      },
      filterByRefundable(refundable, flight) {           
        if (refundable) {
          return flight.refundable 
        }   
        return true        
      },
      filterByForward(forward, flight) {
        let itinerary = flight.itineraries[Object.keys(flight.itineraries)[0]][0]   
        if (forward) {
          return itinerary.stops == 0  
        }        
        return true        
      },  
      filterByBaggage(baggage, flight) {
        let flightBaggage = flight.services[Object.keys(flight.services)[0]]    
        if (baggage) {
          return flightBaggage.code != '0PC'
        } 
        return true               
      },    
      filter(codes, refundable, forward, baggage) {            
        this.filteredFlights = this.flights.filter(flight => this.filterByRefundable(refundable, flight) && this.filterByCarrier(codes, flight) && this.filterByForward(forward, flight) && this.filterByBaggage(baggage, flight))    
      },
      toggleFilters() {
        this.activeFilters = !this.activeFilters
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