<template>
    <Loading v-if="!$store.state.graficos.length > 0" />  <div class="percentual" v-else> 
    <div class="conteudo-charts">

        <b-card>
            <filtroData componente="SET_INICIAL" componente2="SET_FINAL"></filtroData>
        </b-card>
        <hr />
            
        <b-row> 
            <b-col xl="2"></b-col>
            <b-col xl="8" md="12">                
                <PieCarteira />
                <Resumos />
            </b-col>
            <b-col xl="2"></b-col>
        </b-row>

        <b-row> 
            <b-col xl="2"></b-col>
            <b-col xl="8" md="12">
                 
                <br />
                <h4 class="text-center" >Resumo geral</h4>
                <b-table small hover striped outlined :items="$store.state.resumos"></b-table>
      
                 
            </b-col>
            <b-col xl="2"></b-col>
        </b-row>
        
        <b-row> 
            <b-col xl="2"></b-col>
            <b-col xl="4" md="12">
                 <PieDivisao />
            </b-col>
            <b-col xl="4" md="12">
                <PieFiis />
            </b-col>
            <b-col xl="2"></b-col>
        </b-row>

        <b-row>             
            <b-col xl="4" md="12">
                 <PieAcoes />
            </b-col>
            <b-col xl="4" md="12">
                 <PieSmall />
            </b-col>
            <b-col xl="4" md="12">
                 <PieBdrs />
            </b-col>
        </b-row>

         <b-row>             
            <b-col xl="2" md="12">
                 
            </b-col>
            <b-col xl="8" md="12">
                 <ColumnAcoes />                 
            </b-col>
            <b-col xl="2" md="12">
                 
            </b-col>
        </b-row>



    </div>
    </div>
</template>

<script>  
    
    import filtroData from '../utils/filtroData'    
    import Loading from '../../template/Loading'
    import PieCarteira from './pieCarteira'
    import Resumos from '../tabelas/resumo'
    import PieDivisao from './pieDivisaoCarteira'
    import PieFiis from './pieFiis'
    import PieAcoes from './pieAcoes'
    import PieSmall from './pieSmall'
    import PieBdrs from './pieBdrs'
    import ColumnAcoes from './columnAcoes'

    export default {
        
      components: { Loading, filtroData, PieCarteira, Resumos, PieDivisao, PieFiis, PieAcoes, PieSmall, PieBdrs, ColumnAcoes }
    
}
</script>

<style>   

</style>