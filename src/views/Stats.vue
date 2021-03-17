<template>
  <div class="stat">
    <h1>{{  }}</h1>
    <tableSport :region_colors="region_color" @changed="onChangedGraph">
    </tableSport>
    <h1 style="text-align: center;">Muscles distribution</h1>
    <Doughnut
        ref="skillsChart"
        :data="chartData"
        :options="options"
        :i="i"
        >
    </Doughnut>
  </div>
</template>

<script>
import Doughnut from "@/components/Doughnut.vue";
import TableSport from "@/components/TableSport.vue";

const options = {
  responsive: true,
  maintainAspectRatio: false,
  animation: {
    animateRotate: false,
  },
};
export default {
  name: 'Home',
  components:
  {
   Doughnut,
   TableSport
  },
  data () {
    return {
      i:1,
      options,
      region_color: {
        Chest: "yellow",
        Shoulders: "red", 
        Triceps: "blue",
        Legs: "grey",
        Soleus: "green",
        Glutes: "magenta",
        Forearm: "gray",
        Trapezius: "black",
        Back: "cyan"
      },
      chartData: {
        labels: ["Triceps", "Back", "Shoulders"],
        datasets: [{label: "Graph", data: this.data, backgroundColor: ["blue", "green", "yellow"]}]
      }
    }
  },
  methods: {
    onChangedGraph (value) {
      this.i = this.i +1;
      this.data = value;
      this.chartData['datasets'] = [{label: "First Graph", data: Object.values(this.data), backgroundColor: Object.values(this.region_color)}];
      this.chartData['labels'] = Object.keys(this.region_color);
    },
  },
}
</script>
