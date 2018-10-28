<template>
     <div>
      <a href="" @click.prevent="fetchResource">Fetch</a><br/>
     <apexcharts width="500" type="line" :options="chartOptions" :series="series"></apexcharts>

      <h2>{{resources}}</h2>
     <p>{{error}}</p>
    </div>
</template>

<script>
import VueApexCharts from 'vue-apexcharts'
import $backend from '../backend'

export default {
  components: {
    apexcharts: VueApexCharts
  },
  data: function () {
    return {
      resources: [],
      error: '',
      chartOptions: {
        chart: {
          height: 350,
          shadow: {
            enabled: true,
            color: '#000',
            top: 18,
            left: 7,
            blur: 10,
            opacity: 1
          },
          zoom: {
            enabled: false
          }
        },
        colors: ['#77B6EA', '#545454'],
        dataLabels: {
          enabled: true
        },
        stroke: {
          curve: 'smooth'
        },
        markers: {
          style: 'inverted',
          size: 6
        },
        xaxis: {
          categories: ['1', '2', '3', '4', '5', '6', '7', '8', '9', '10', '11', '12'],
          title: {
            text: 'Month'
          }
        },
        yaxis: {
          title: {
            text: 'Temperature'
          },
          min: 5,
          max: 40
        },
        legend: {
          position: 'top',
          horizontalAlign: 'right',
          floating: true,
          offsetY: -25,
          offsetX: -5
        },
        grid: {
          borderColor: '#e7e7e7',
          row: {
            colors: ['#f3f3f3', 'transparent'], // takes an array which will be repeated on columns
            opacity: 0.5
          }
        }
      },
      series: [{
        name: 'High - 2013',
        data: [28, 29, 33, 36, 32, 32, 33]
      },
      {
        name: 'Low - 2013',
        data: [12, 11, 14, 18, 17, 13, 13]
      }
      ]

    }
  },
  methods: {
    fetchResource () {
      $backend.fetchSentiment()
        .then(responseData => {
          this.resources.push(responseData)
        }).catch(error => {
          this.error = error.message
        })
    }
  }
}
</script>
