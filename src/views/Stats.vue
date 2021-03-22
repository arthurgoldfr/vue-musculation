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
        Chest: "Gold",
        Shoulders: "#8B0000", 
        Triceps: "#E6E6FA",
        Legs: "#00008B",
        Soleus: "MediumSpringGreen",
        Glutes: "#E9967A",
        Forearm: "#ADFF2F",
        Trapezius: "#556B2F",
        Back: " #2F4F4F"
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
