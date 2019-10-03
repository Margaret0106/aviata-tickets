<template>
  <div class="tickets-list__item ticket">
    <div class="ticket__content">
      <div class="ticket__info">
        <div class="carrier">
          <div class="carrier__logo">
            <img src="https://aviata.kz/static/airline-logos/80x80/KC.png" alt="">
          </div>
          <div class="carrier__title">Air Astana</div>
        </div>
        <div class="flight">
          <div class="flight__datetime">
            <span class="date">25 ноя, вс</span>
            23:25
          </div>
          <div class="flight__itinerary">
            <div class="flight__info">
              <span class="airport-name">ALA</span>
              <div class="flight__duration">4 ч 20 м</div>
              <span class="airport-name">TSE</span>
            </div>
            <div class="flight__line">
              <span></span>
            </div>
            <div class="flight__transfer">
              через Шымкент, 1 ч 50 м
            </div>            
          </div>
          <div class="flight__datetime">
            <span class="date">26 ноя, сб</span>
            03:45
            <sup>+1</sup>
          </div>
        </div>
      </div>
      <div class="ticket__details">
        <a href="" class="ticket__link">Детали перелета</a>
        <a href="" class="ticket__link">Условия тарифа</a>
        <span class="non-refund">Невозвратный</span>
      </div>           
    </div>
    <div class="ticket__price">
      <div class="price">590 240 ₸</div>
      <button class="btn btn--green ticket__button">Выбрать</button>
      <div class="price-info">Цена за всех пассажиров</div>
      <div class="baggage-info">
        <span>Нет багажа</span>
        <button class="btn btn--small btn--blue">
        + Добавить багаж
        </button>    
      </div>
    </div>
  </div>
</template>

<script>
   export default {
    name: 'ticket',
    props: {
      flight: Object,
      airlines: Object,
    },
    data: function() {
      return {
        carrier_name: this.flight
      }
    }   
  }
</script>

<style lang="scss" src="../assets/styles/buttons.scss"/>
