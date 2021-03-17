<script>
import { Doughnut } from 'vue-chartjs'

export default {
  extends: Doughnut,
  props: ["data", "options", "i"],
  mounted() {
    this.renderDoughnutChart();
  },
  computed: {
    chartData: function() {
      console.log("computed")
      console.log(this.data)
      return this.data;
    }
  },
  methods: {
    renderDoughnutChart: function() {
      console.log(this.chartData)
      console.log("renderDoughnut")
      this.renderChart(
        {
          labels:  this.chartData["labels"],
          datasets: this.chartData["datasets"],
        },
        {
          responsive: true, maintainAspectRatio: false
        }
      );        
    }
  },
  watch: {
    i: function() 
    { console.log("hey")
      console.log(this.chartData)           
      this.renderDoughnutChart()  
    }
  }
};
</script>
