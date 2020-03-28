<template>
  <ve-line :data="chartData" :extend="chartSettings" :settings="chartSettings"></ve-line>
</template>

<script>
export default {
  data () {
    this.chartSettings = {
      axisSite: { right: ['CV', 'CPA'] },
      yAxisType: ['normal', 'normal'],
      yAxisName: ['CNY', 'CV/CPA'],
      series: {
        label: {
          normal: {
            show: true
          }
        }
      },
      labelMap: {
        CNY: '消耗',
        CV: '加粉',
        CPA: '成本'
      }
    }
    return {
      chartData: {
        columns: ['date', 'CNY', 'CV', 'CPA'],
        rows: [
          { date: '1/1', CNY: 1393, CV: 13, CPA: 110 },
          { date: '1/2', CNY: 3530, CV: 35, CPA: 90 },
          { date: '1/3', CNY: 2923, CV: 39, CPA: 85 },
          { date: '1/4', CNY: 1723, CV: 17, CPA: 101 },
          { date: '1/5', CNY: 3792, CV: 38, CPA: 99 },
          { date: '1/6', CNY: 4593, CV: 46, CPA: 95 }
        ]
      }
    }
  }
}
</script>
