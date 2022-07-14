<template>
  <div>
    <div class="table">
        <b-table style="text-align: center;"
        bordered
              outlined
              striped
              hover
              :items="musics"
              :filter="filter"
              :fields="fields"
        >
        </b-table>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
    name:'music',
    props:['items'],
    data(){
        return {
            musics:[],
            apiURL :'http://localhost:1337/api/music',
            filter:'',
            fields:[
                {key: 'id',labal :'ID' ,sortable: true, tdClass: 'center' },
                {key: 'attributes.name', label: 'NAME', tdClass: 'center' },
                {key: 'attributes.time', label: 'TIME', tdClass: 'center' },
            ]
        }
    },
    async mounted(){
        const result = await axios.get(this.apiURL)
        this.musics= result.data.data
        
    }
}
</script>

<style>

</style>