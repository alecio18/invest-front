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
            </b-col>
            <b-col xl="2"></b-col>
        </b-row>

        <b-row> 
            <b-col xl="2"></b-col>
            <b-col xl="8" md="12">
                 
            </b-col>
            <b-col xl="2"></b-col>
        </b-row>
        
        <b-row> 
            <b-col xl="2"></b-col>
            <b-col xl="8" md="12">
                 
            </b-col>
            <b-col xl="2"></b-col>
        </b-row>

    </div>
    </div>
</template>

<script>  
    
    import filtroData from '../utils/filtroData'    
    import Loading from '../../template/Loading'
    import PieCarteira from './pieCarteira'

    export default {
        
      components: { Loading, filtroData, PieCarteira }
    
}
</script>

<style>   

</style>