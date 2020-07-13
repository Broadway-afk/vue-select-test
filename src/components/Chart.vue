<script>
  import { Line } from 'vue-chartjs'

  export default {
    extends: Line,
    props: [
      'data'
    ],
    mounted () {
      this.renderChart({
        labels: ['2015', '2016', '2017', '2018', '2019', '2020'],
        datasets: [{
          label: 'Focus',
          data: this.data.focus,
          backgroundColor: [
            'rgba(255, 99, 132, 0.2)',
          ],
          borderColor: [
            'rgba(255, 99, 132, 1)',
          ],
          borderWidth: 2
        },
        {
          label: 'Scope',
          data: this.data.scope,
          backgroundColor: [
            'rgba(54, 162, 235, 0.2)'
          ],
          borderColor: [
            'rgba(54, 162, 235, 1)'
          ],
          borderWidth: 2
        }]
      }, {
        responsive: true,
        maintainAspectRatio: false
      });
    }
  }
</script>