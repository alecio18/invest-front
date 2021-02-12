<template>
    <div id="smallpie">
        
    </div>
</template>

<script>

import storeData from '../utils/storeData'

import Highcharts from 'highcharts'
import exportingInit from 'highcharts/modules/exporting'

import padrao from 'highcharts/themes/grid-light'

export default {
    
   extends: storeData,
    
    methods: {

        dataSource() {
                           
           let charts = this.$store.state.graficos 

           let serie = []
           let rotativoLoopCharts =[]
            Object.entries(charts).forEach(([,valor]) => { 
                if(valor.tipo == "SMALL"){

                   let x = String(valor.p_total).replace(',','.')

                   let y = parseFloat(x)

                    rotativoLoopCharts = {                                              
                        'y' : y,
                        'name' : valor.acao,                                                                    
                    }
                    serie.push(rotativoLoopCharts)  
                }             
           }) 

           this.setup({ serie }) 
          
        },
    
        setup(obj){
            

            const { serie } = obj
           
           // Iniciando serviço para impressão
           exportingInit(Highcharts)

            // Aplicando o Tema
            
            padrao(Highcharts)
            
            Highcharts.chart("smallpie", {

                credits: {
                     enabled: false
                },          

                // Inicio da Plotagem do Grafico

                chart: {
                    type: 'pie', 
                    plotShadow: false,                   
                },
                title: {
                    text: 'Small CAPS'
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