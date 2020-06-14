<script>
import { Line, mixins } from "vue-chartjs";

const { reactiveProp } = mixins;

export default {
  extends: Line,
  mixins: [reactiveProp],

  props: {
    options: Object,
  },

  mounted() {
    this.renderChart(this.chartData, this.options);
  },
};
</script>

<style scoped>
canvas {
  display: block;
  max-width: 1200px;
  /* max-height: 600px; */
  margin: auto;
}
</style>
