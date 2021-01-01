<template>
  <div class="home">
    <tableSport/>
    <RandomChart/>
  </div>
</template>

<script>
import RandomChart from "@/components/RandomChart.vue";
import TableSport from "@/components/TableSport.vue";
export default {
  name: 'Home',
  components:
  {
   RandomChart,
   TableSport
  }
}
</script>
