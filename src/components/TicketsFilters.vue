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
          <label v-for="(value, name) in airlines" :key="name" class="filter__option">
            <input v-model="checkedCarriers" :value="name" type="checkbox">
            <span class="checkbox"></span>
            {{value}}
          </label>
        </vuescroll>        
      </div>
    </div>
    <a href="" class="reset-filters" @click.prevent="resetFilters">Сбросить все фильтры</a>
  </div>
</template>


<script> 
  import vuescroll from 'vuescroll';

  export default {
    name: 'tickets-filters',
    components: {     
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
        type: Object,
        default: () => {}
      },
      active: {
        type: Boolean,
        default: () => false
      }
    },
    methods: {
      filterFlights() {
        this.$emit('filter', this.checkedCarriers, this.checkedRefundable, this.checkedForward, this.checkedBaggage)
      },
      resetFilters() {           
        this.checkedCarriers = [],
        this.checkedRefundable = false,
        this.checkedForward = false,
        this.checkedBaggage = false
      }
    },
    watch: {
      checkedCarriers() {
        this.filterFlights()
      },
      checkedRefundable() {
        this.filterFlights()
      },
      checkedBaggage() {
        this.filterFlights()
      },
      checkedForward() {
        this.filterFlights()
      },

    }
  }
</script>

<style lang="scss" src="../assets/styles/filters.scss" />