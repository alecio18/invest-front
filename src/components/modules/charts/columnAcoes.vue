<template>
    <div id="columnacoes">
        
    </div>
</template>

<script>

import storeData from '../utils/storeData'

import Highcharts from 'highcharts'
import exportingInit from 'highcharts/modules/exporting'

import padrao from 'highcharts/themes/grid-light'
import _ from 'lodash'

export default {
    
   extends: storeData,
    
    methods: {

        dataSource() {
                           
           let charts = this.$store.state.graficos 

           let series = []
           let rotativoLoopCharts =[]
            Object.entries(charts).forEach(([,valor]) => {                 

                   let x = String(valor.p_total).replace(',','.')

                   let y = parseFloat(x)

                    rotativoLoopCharts = {                                              
                        'y' : y,
                        'name' : valor.acao,                                                                    
                    }
                    series.push(rotativoLoopCharts)  
                            
           }) 
           
           let serie = _.orderBy(series, ['y'], ['desc'])

           const categories = serie.map(item => item.name)
           const data = serie.map(item => item.y )
           

           this.setup({ data, categories }) 
          
        },
    
        setup(obj){

            const { data, categories } = obj
           
           // Iniciando serviço para impressão
           exportingInit(Highcharts)

            // Aplicando o Tema
            
            padrao(Highcharts)
            
            Highcharts.chart("columnacoes", {

                credits: {
                     enabled: false
                },          

                // Inicio da Plotagem do Grafico

                chart: {
                    type: 'column', 
                    plotShadow: false,                   
                },
                title: {
                    text: 'Lista Ações'
                },
                xAxis: {
                    categories: categories,
                    crosshair: true
                 },
                 yAxis: {
                     min: 0,
                     title: {
                         text: 'Valor'
                     }
                 },
                 tooltip: {
                    pointFormat: '<tr><td style="color:{series.color};padding:0">{series.name}: </td>' +
                        '<td style="padding:0"><b>{point.y:.2f}</b></td></tr>',
                 },
                              
                plotOptions: {
                    pie: {
                        cursor: 'pointer',
                        allowPointSelect: false,
                        dataLabels: {
                            enabled: true,
                            format: '<b>{point.name}  </b> : {point.percentage:.2f} %'
                        },
                        showInLegend: true
                    },
                    
                },
                series: [{                        
                        name: "Ações", 
                        colorByPoint: true,                       
                        data: data,                        
                }]
            });

        }

    }

}

</script>

<style>

</style>