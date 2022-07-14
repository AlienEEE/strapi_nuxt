<template>
  <div>
    <div class="table">
        <b-table style="text-align: center; 
"
        bordered
              outlined
              striped
              hover
              :items="singers"
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
    name:'singer',
    props:['items'],
    data(){
        return {
            singers:[],
            apiURL :'http://localhost:1337/api/singers',
            filter:'',
            fields:[
                {key: 'id',labal :'ID' ,sortable: true, tdClass: 'center' },
                {key: 'attributes.name', label: 'NAME', tdClass: 'center' },
                {key: 'attributes.des', label: 'DES', tdClass: 'center' },
            ]
        }
    },
    async mounted(){
        const result = await axios.get(this.apiURL)
        this.singers = result.data.data
       
    }
}
</script>

<style>

</style>