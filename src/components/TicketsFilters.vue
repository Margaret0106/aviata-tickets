<template>
  <div class="tickets__filters filters">
    <div class="filters__item">
      <h4 class="filters__title">Опции тарифа</h4>
      <div class="filter">
        <label class="filter__option">
          <input type="checkbox">
          <span class="checkbox"></span>
          Только прямые
        </label>
        <label class="filter__option">
          <input type="checkbox">
          <span class="checkbox"></span>
          Только с багажом
        </label>
        <label class="filter__option">
          <input type="checkbox">
          <span class="checkbox"></span>
          Только возвратные
        </label>
      </div>      
    </div>
    <div class="filters__item">
      <h4 class="filters__title">Авиакомпании</h4>
      <div class="filter">  
        <checkbox 
          v-for="(value, index) in airlines" 
          v-bind:key="index"
          v-bind:item="value">        
        </checkbox>       
      </div>      
    </div>
  </div>
</template>      


<script>
  import Checkbox from './ui/Checkbox.vue'

  export default {
    name: 'tickets-filters',
    components: {
      Checkbox
    },
    props: {
      airlines: {
        type: Object
      }
    }   
  }
</script>

<style lang="scss" src="../assets/styles/filters.scss"/>
