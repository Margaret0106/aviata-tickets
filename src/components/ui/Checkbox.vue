<template>
  <label class="filter__option">
    <input 
      type="checkbox" 
      :value="val"  
      v-on:input="$emit('input', $event.target.value)"
    >
    <span class="checkbox"></span>
    {{item}}
  </label>
</template>


<script> 
  export default {
    name: 'checkbox',
    props: ['item', 'val']   
  }
</script>

