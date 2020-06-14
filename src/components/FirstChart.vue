<script>
import { Line } from "vue-chartjs";

const data = {
  labels: ["date1", "date2", "date3"],
  datasets: [
    {
      label: "My First dataset",
      backgroundColor: "rgba(0, 0, 0, 0)",
      borderColor: "rgb(255, 99, 132)",
      data: [0, 10, 5],
    },
  ],
};

const options = {};

export default {
  extends: Line,

  mounted() {
    this.renderChart(data, options);
  },
};
</script>

<style scoped>
canvas {
  max-width: 1200px;
  max-height: 600px;
  margin: auto;
}
</style>
