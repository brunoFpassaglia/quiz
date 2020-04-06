<template>
  <b-nav tabs="">
    <b-nav-item active disabled="">Fancy quiz app</b-nav-item>
    <b-nav-item disabled="">Counter:{{numCorrect}}/{{numTotal}}</b-nav-item>
  </b-nav>
</template>


<script>
export default {
  props: [
    'numCorrect',
    'numTotal'  
  ]
}
</script>