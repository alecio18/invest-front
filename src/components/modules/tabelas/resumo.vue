<template>
    <div id="resumos">
      
    </div>
</template>

<script>

import storeData from '../utils/storeData'
import _ from 'lodash'

export default {
    
   extends: storeData,
    
    methods: {

        dataSource() {
                           
           let charts = this.$store.state.graficos            
           let resumo = []
           let rotativoLoopCharts =[]
            
            Object.entries(charts).forEach(([,valor]) => { 
                rotativoLoopCharts = {  
                       'acao' : valor.acao,
                       'quantidade' : valor.qtd,
                       'preco_medio' : "R$ " + parseFloat(String(valor.pm).replace(',','.')).toFixed(2),
                       'preco_total' : "R$ " + parseFloat(String(valor.p_total).replace(',','.')).toFixed(2),
                       'tipo' : valor.tipo                                                 
                   }
                resumo.push(rotativoLoopCharts)                     
                         
           })           
        
            let resumoOrder = _.orderBy(resumo, 'tipo')

        this.$store.commit('SET_RESUMOS', resumoOrder) 
        
        }
    }

}

</script>

<style>

</style>