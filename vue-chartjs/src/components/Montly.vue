<template>
    <canvas class="chart" ref="mixedChart"></canvas>
  </template>
  
  <script setup>
  import { onMounted, ref } from 'vue';
  import { Chart } from 'chart.js/auto';
  import annotationPlugin from 'chartjs-plugin-annotation';
  
  Chart.register(annotationPlugin);
  
  const calculateAverage = (data) => {
    const sum = data.reduce((a, b) => a + b, 0);
    return sum / data.length;
  };
  
  const mixedChart = ref(null);
  
  const valueToLabel = (value) => {
    if (value >= 10) {
      return 'High';
    } else if (value >= 5) {
      return 'Medium';
    } else {
      return 'Low';
    }
  };
  
  const chartData = {
    labels: [
      '1', '2', '3', '4', '5', '6', '7', '8', '9', '10',
      '11', '12', '13', '14', '15', '16', '17', '18', '19', '20',
      '21', '22', '23', '24', '25', '26', '27', '28', '29', '30', '31'
    ],
    datasets: [
      {
        type: 'bar',
        label: 'Bar',
        data: [
          3, 5, 2, 3, 7, 4, 5, 3, 5, 2,
          3, 7, 2, 4, 6, 3, 5, 2, 4, 6,
          3, 5, 7, 2, 4, 6, 3, 5, 2, 4, 6
        ],
        backgroundColor: ['rgba(47, 224, 74, 0.5)'],
        borderColor: ['rgba(47, 224, 74, 1)'],
        borderWidth: 1,
      },
      {
        type: 'line',
        label: 'Line',
        data: [
          3, 5, 2, 3, 7, 4, 5, 3, 5, 2,
          3, 7, 2, 4, 6, 3, 5, 2, 4, 6,
          3, 5, 7, 2, 4, 6, 3, 5, 2, 4, 6
        ],
        borderColor: 'rgba(47, 224, 74, 0.8)',
        borderWidth: 2,
        fill: false,
        tension: 0.1,
        pointBackgroundColor: 'rgba(47, 224, 74, 1)',
        pointBorderColor: 'rgba(47, 224, 74, 1)', 
        pointRadius: 2.5
      },
    ],
  };
  
  const chartOptions = {
    scales: {
      y: {
        beginAtZero: true,
        title: {
          display: true,
          text: 'Emotion Level',
          font: {
            size: 16,
            family: 'Helvetica',
            weight: 'bold',
          },
          color: 'black',
        },
        ticks: {
          callback: valueToLabel, 
          maxTicksLimit: 3, 
        },
      },
      x: {
        title: {
          display: true,
          text: 'Monthly',
          font: {
            size: 16,
            family: 'Helvetica',
            weight: 'bold',
          },
          color: 'black',
        },
      },
    },
    plugins: {
      legend: {
        display: false,
      },
      annotation: {
        annotations: {
          averageLine: {
            type: 'line',
            scaleID: 'y',
            value: calculateAverage(chartData.datasets[0].data), 
            borderColor: 'rgba(47, 224, 74, 0.5)',
            borderWidth: 2,
            borderDash: [5, 5],
            label: {
              enabled: true,
              content: 'Average',
              position: 'end',
              backgroundColor: 'rgba(47, 224, 74, 0.5)',
              color: 'black',
              font: {
                size: 12,
                family: 'Helvetica',
                weight: 'bold',
              },
            },
          },
        },
      },
      tooltip: {
        callbacks: {
          label: (context) => {
            const value = context.raw;
            return `Emotion Level = ${value}`;
          },
        },
      },
    },
  };
  
  onMounted(() => {
    new Chart(mixedChart.value, {
      type: 'bar', 
      data: chartData,
      options: chartOptions,
    });
  });
  </script>
  
  <style scoped>
  .chart {
    margin: 10px;
  }
  </style>
  