<template>
  <div class="tickets-list__item ticket">
    <div class="ticket__content">
      <div class="ticket__info">
        <div class="carrier">
          <div class="carrier__logo">
            <img :src="`https://aviata.kz/static/airline-logos/80x80/${flight.validating_carrier}.png`" alt="">
          </div>
          <div class="carrier__title">{{itinerary.carrier_name}}</div>
        </div>
        <div class="flight">
          <div class="flight__datetime">            
            <span class="date">{{itinerary.dep_date | getFlightDay}}</span>
            {{itinerary.dep_date | getFlightTime}}
          </div>
          <div class="flight__itinerary">
            <div class="flight__info">
              <span class="airport-name">{{getAirports.firstAirport.origin_code}}</span>
              <div class="flight__duration">{{ flight.best_time | formatTime }}</div>
              <span class="airport-name">{{getAirports.lastAirport.dest_code}}</span>
            </div>
            <div class="flight__line">
              <span></span>
            </div>
            <div class="flight__transfer">
              <span v-if="itinerary.stops == 0" class="green">
                прямой рейс
              </span>
              <span v-else-if="itinerary.stops > 1">
                Пересадок: {{itinerary.stops}}
              </span>
              <span v-else>
                через {{getAirports.lastAirport.origin}}, <br> 
                стык. {{layover | formatTime}}
              </span>              
            </div>            
          </div>
          <div class="flight__datetime">
            <span class="date">{{itinerary.arr_date | getFlightDay}} 
              <span v-if="diffDays > 0" class="diff-days">+{{diffDays}}</span>
            </span>    
            {{itinerary.arr_date | getFlightTime}}             
          </div>
        </div>
      </div>
      <div class="ticket__details">
        <a href="" class="ticket__link">Детали перелета</a>
        <a href="" class="ticket__link">Условия тарифа</a>
        <span v-if="flight.refundable == false" class="non-refund"> <img src="../assets/icon-non-refundeble.svg" alt="">Невозвратный</span>
      </div>           
    </div>
    <div class="ticket__price">
      <div class="price">{{flight.price}} ₸</div>
      <button class="btn btn--green ticket__button">Выбрать</button>
      <div class="price-info">Цена за всех пассажиров</div>
      <div class="baggage-info">
        <div v-if="baggage.code == '0PC'">
          <span>Нет багажа</span>   
          <button class="btn btn--small btn--blue">
          + Добавить багаж
          </button>        
        </div>
        <span v-else>Багаж: {{baggage.alt_text}}</span>        
      </div>
    </div>
  </div>
</template>

<script>

   export default {
    name: 'ticket',
    props: {
      flight: Object
    },
    data: function() {
      return {
        hasLayover: null,
        hasBaggage: null,
        isRefundable: null
      }
    },       
    filters: {
      formatTime: function (value) {
        if (!value) return ''
        let hours, minutes, totalseconds
        hours = Math.floor(value / 3600)
        totalseconds = value % 3600
        minutes = Math.floor(totalseconds / 60)
        return `${hours} ч ${minutes} м`        
      },
      getFlightTime: function (value) {
        const date = new Date(value)
        const leadingZero = (num) => `0${num}`.slice(-2);

        const formatedTime = (date) =>
          [date.getHours(), date.getMinutes()]
          .map(leadingZero)
          .join(':');

        return formatedTime(date)
      },
      getFlightDay: function (value) {
        const weekDays = ['вс','пн','вт','ср','чт','пт','сб'] 
        const months = ['янв','фев','мар','апр','мая','июн','июл','авг','сен','окт','ноя','дек']  
        const date = new Date(value)

        let day = date.getDate()
        let month = months[date.getMonth()]
        let weekDay = weekDays[date.getDay()]

        return `${day} ${month}, ${weekDay}`
      }      
    },
    computed: {
      baggage: function () {
        if (!this.flight.services) return []       
        return this.flight.services[Object.keys(this.flight.services)[0]]        
      },
      itinerary: function () {
        if (!this.flight.itineraries) return []       
        return this.flight.itineraries[Object.keys(this.flight.itineraries)[0]][0]
      },  
      getAirports: function () {
        if (!this.itinerary) return [] 
        const segments = this.itinerary.segments        
        const segmentsArray = Object.keys(segments)        
        const firstSegment = segments[segmentsArray[0]]
        const lastSegment = segmentsArray.length > 1 ? segments[segmentsArray[segmentsArray.length - 1]] : firstSegment

        const airports = {
          firstAirport: firstSegment,
          lastAirport: lastSegment
        }
        return airports
      },
      layover: function () {        
        if (!this.itinerary.layovers) return [] 
        return this.itinerary.layovers[Object.keys(this.itinerary.layovers)[0]]
      },
      diffDays: function () {
        const date1 = new Date(this.itinerary.dep_date);
        const date2 = new Date(this.itinerary.arr_date);
        const diffDays = Math.abs(date2.getDate() - date1.getDate());   
        return diffDays        
      }     
    } 
  }
</script>

<style lang="scss" src="../assets/styles/buttons.scss"/>
