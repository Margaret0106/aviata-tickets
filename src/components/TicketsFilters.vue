<template>
  <div class="tickets__filters filters" :class="{active: active}">
    <div class="filters__item">
      <h4 class="filters__title">Опции тарифа</h4>
      <div class="filter">
        <label class="filter__option">
          <input type="checkbox" value="forward" v-model="checkedForward">
          <span class="checkbox"></span>
          Только прямые
        </label>
        <label class="filter__option">
          <input type="checkbox" value="baggage" v-model="checkedBaggage">
          <span class="checkbox"></span>
          Только с багажом
        </label>
        <label class="filter__option">
          <input type="checkbox" value="refundable" v-model="checkedRefundable">
          <span class="checkbox"></span>
          Только возвратные
        </label>
      </div>
    </div>
    <div class="filters__item">
      <h4 class="filters__title">Авиакомпании</h4>
      <div class="filter filter--scrollable">
        <vuescroll :ops="ops">
          <label class="filter__option" :key="name" v-for="(value, name) in airlines">
            <input type="checkbox" :value="name" v-model="checkedCarriers">
            <span class="checkbox"></span>
            {{value}}
          </label>
        </vuescroll>        
      </div>
    </div>
    <a href="" class="reset-filters" v-on:click="resetFilters">Сбросить все фильтры</a>
  </div>
</template>


<script>
  // import Checkbox from './ui/Checkbox.vue'
  import vuescroll from 'vuescroll';

  export default {
    name: 'tickets-filters',
    components: {
      // Checkbox
      vuescroll
    },
    data: function () {
      return {
        ops: {
          rail: {
            keepShow: true
          },
          bar: {
            onlyShowBarOnScroll: false,
            keepShow: true,
            background: '#E1E1E1',
            size: '4px',
            specifyBorderRadius: '2px'
          },         
          vuescroll: {
            wheelScrollDuration: 100
          }
        },
        checkedCarriers: [],
        checkedRefundable: false,
        checkedForward: false,
        checkedBaggage: false
      }
    },
    props: {
      airlines: {
        type: Object
      },
      active: {
        type: Boolean
      }
    },
    methods: {
      filterFlights: function () {
        this.$emit('filter', this.checkedCarriers, this.checkedRefundable, this.checkedForward, this.checkedBaggage)
      },
      resetFilters: function (e) {
        e.preventDefault();        
        this.checkedCarriers = [],
        this.checkedRefundable = false,
        this.checkedForward = false,
        this.checkedBaggage = false
      }
    },
    watch: {
      checkedCarriers: function () {
        this.filterFlights()
      },
      checkedRefundable: function () {
        this.filterFlights()
      },
      checkedBaggage: function () {
        this.filterFlights()
      },
      checkedForward: function () {
        this.filterFlights()
      },

    }
  }
</script>

<style lang="scss" src="../assets/styles/filters.scss" />