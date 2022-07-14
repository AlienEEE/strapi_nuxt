<template>
  <div>
    <div class="table" >
        <b-table style="text-align: center;  
"
        bordered
              outlined
              striped
              hover
              :items="instruments"
              :filter="filter"
              :fields="fields"
        >
        </b-table>
    </div>
    <div v-for="i in instruments " :key="i.id" >
        <img :src="imgs">
  </div>
   </div>
</template>

<script>
import axios from "axios";
export default {
    name:'instrument',
    props:['items'],
    data(){
        return {
            instruments:[],
            imgs:[],
            apiURL :'http://localhost:1337/api/instruments?populate=img',
            filter:'',
            fields:[
                {key: 'id',labal :'ID' ,sortable: true, tdClass: 'center' },
                {key: 'attributes.name', label: 'NAME', tdClass: 'center' },
                {key: 'attributes.img.data[0].attributes.url', label: 'IMG', tdClass: 'center' },
            ]
        }
    },
    async mounted(){
        const result = await axios.get(this.apiURL)
        this.instruments = result.data.data
        console.log(this.instruments);
        console.log(this.instruments[1].attributes.img.data[0].attributes.url);
        let i=0;
        this.imgs="http://localhost:1337" +this.instruments[i].attributes.img.data[0].attributes.url;
        console.log(this.imgs);

    },
}
</script>

<style>

</style>