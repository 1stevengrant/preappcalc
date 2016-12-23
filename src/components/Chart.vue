<template>
	
	<div id="Chart" style="height: 300px"></div>

</template>

<script>
import Highcharts from 'highcharts'

export default {
	name: 'Chart',
	props: ['chartType', 'chartTitle', 'labels', 'values'],
	mounted () {
		var highchartsOptions = {
    		chart: {
		    	type: this.chartType
		  	},
		  	title: {
		    	text: this.chartTitle
		  	},
		  	xAxis: {
		  		allowDecimals: false,
		  		title: {
		  			text: 'Age'
		  		},
		  		labels: {
						formatter: function () {
							return this.labels;
						}
          }
		  	},
		  	yAxis: {
		  		title: {
		  			text: 'Pot Value'
		  		},
		  		labels: {
            formatter: function () {
                return this.value + 'k';
            }
          },
		    	opposite: true
		  	},
			  series: [{
			    name: 'Pot Value',
			      data: this.values
			  }]
    }
		Highcharts.chart('Chart', highchartsOptions)
	},
}
</script>