<template>
  <label class="filter__option">
    <input type="checkbox">
    <span class="checkbox"></span>
    {{item}}
  </label>
</template>


<script> 
  export default {
    name: 'checkbox',
    props: ['item']   
  }
</script>

