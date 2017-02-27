<template>
	
	<div style="height: 300px"></div>

</template>

<script>
import Highcharts from 'highcharts'

export default {
	name: 'Chart',
	props: ['chartType', 'chartTitle', 'yAxisTitle', 'xAxisTitle', 'agePotValue'],
	mounted () {
		var highchartsOptions = {
			chart: {
				type: 'area'
			},
			credits: {
				enabled: false
			},
			tooltip: {
				enabled: false
			},
			title: {
				text: ''
			},
			xAxis: {
				allowDecimals: false,
				title: {
					text: 'Age'
				}
			},
			yAxis: {
				title: {
				  text: 'Pot Value'
				},
				labels: {
					formatter: function () {
				    return '£' + this.value / 1000 + 'k';
				  }
				},
				opposite: true,
			},
			plotOptions: {},
			series: [{
				name: 'Pot Value at Age',
				data: this.agePotValue
			}],
			credits: false
    	}
		Highcharts.chart(this.$el, highchartsOptions)
	},
}
</script>