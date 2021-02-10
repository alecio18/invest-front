<template>
    <div id="divisaoCarteira">
        
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
                           
           let chart = this.$store.state.graficos 

           

            let charts = _.orderBy(chart, 'tipo')

            
            let serie = []
            let rotativoLoopCharts =[]
            let somaAcoes = 0
            let tipo = ''            
            let cont = 0
            let contTotal = 1 
            let x = 0
            
            Object.entries(charts).forEach(([,valor]) => { 
                
               if (cont == 0){
                   tipo = (valor.tipo)
               } 
               if (tipo != valor.tipo){
                
                rotativoLoopCharts = {                                              
                       'y' : somaAcoes,
                       'name' : tipo,                                                                    
                   }
                serie.push(rotativoLoopCharts) 
                rotativoLoopCharts = {}
                somaAcoes = 0
                cont = 0
                tipo = valor.tipo
               }            

               if (tipo == valor.tipo){
                   let y = String(valor.p_total).replace(',','.')

                   x = parseFloat(y)                   
                   somaAcoes += x                  
                   cont++
               }
                if (charts.length == contTotal){

                   rotativoLoopCharts = {
                       'y' : somaAcoes,
                       'name' : valor.tipo, 
                    }
                  serie.push(rotativoLoopCharts)

               }   

               contTotal++
           }) 

           serie           

           this.setup({ serie }) 
          
        },
    
        setup(obj){
            

            const { serie } = obj
           
           // Iniciando serviço para impressão
           exportingInit(Highcharts)

            // Aplicando o Tema
            
            padrao(Highcharts)
            
            Highcharts.chart("divisaoCarteira", {

                credits: {
                     enabled: false
                },          

                // Inicio da Plotagem do Grafico

                chart: {
                    type: 'pie', 
                    plotShadow: false,                   
                },
                title: {
                    text: 'Carteira'
                },
                 tooltip: {
                    pointFormat: '<tr><td style="color:{series.color};padding:0">{series.name}: </td>' +
                        '<td style="padding:0"><b>{point.y:.2f}</b></td></tr>',
                 },
                              
                plotOptions: {
                    pie: {
                        cursor: 'pointer',
                        allowPointSelect: true,
                        dataLabels: {
                            enabled: true,
                            format: '<b>{point.name}  </b> : {point.percentage:.2f} %'
                        },
                        showInLegend: true
                    },
                    
                },
                series: [{                        
                        name: "R$ ", 
                        colorByPoint: true,                       
                        data: serie
                }]
            });

        }

    }

}

</script>

<style>

</style>