<template>
  <div class="home">
    <h1>{{  }}</h1>
    <tableSport :region_colors="region_color" @changed="onChangedGraph">
    </tableSport>
    <Doughnut
        ref="skillsChart"
        :chart-data="chartData"
        :options="options">
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
      data: {
      },
      chartData: {
        datasets: [{label: "Graph", data: this.data, backgroundColor: ["blue", "green", "yellow"]}],
        labels: ["Triceps", "Back", "Shoulders"]
      }
    }
  },
  methods: {
    onChangedGraph (value) {
      this.data = value;
      this.chartData['datasets'] = [{label: "First Graph", data: Object.values(this.data), backgroundColor: Object.values(this.region_color)}];
      this.chartData['labels'] = Object.keys(this.region_color);
    }
  }
}
</script>
