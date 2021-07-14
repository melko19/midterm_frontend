<template>
    <div class="bgd">
        <Navbar />
        <EditInstrumentModal :instrument="selectedInstrument"/>
        <DeleteInstrumentModal :instrument="selectedInstrument" @onDeleted="getAll"/>
        <div class="container">
            <h1>
                <br>                
                Music Instruments
                <InstrumentEntryModal class="float-right" @onAdd="getAll"/>
                </h1>
            <table class="table table-boredered">
                <thead>
                    <tr class="bg-info text-white">
                        <th>Name</th>
                        <th>Type</th>
                        <th>Definition</th>
                        <th>Price</th>
                        <th>Range</th>
                        <th>&nbsp;</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="instrument in instruments" :key="instrument.id">
                        <td>{{instrument.name}}</td>
                        <td>{{instrument.type}}</td>
                        <td>{{instrument.definition}}</td>
                        <td>{{instrument.price}}</td>
                        <td>{{instrument.range}}</td>
                        <td>
                            <b-button @click="onEdit(instrument)" variant="info" size="sm">
                                Edit
                            </b-button>

                            <b-button @click="onDelete(instrument)" variant="danger" size="sm">
                                Delete
                            </b-button>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>
<script>
export default {
    data(){
        return{
            instruments: [],
            selectedInstrument:{}
        }
    },
    methods: {
        async getAll(){
            await this.$axios.get('/api/instruments')
            .then((res)=>{
                if(res.status==200){
                    this.instruments = res.data

                }
            })
        },
        onEdit(selectedInstrument){
            this.selectedInstrument = selectedInstrument;
            this.$bvModal.show('editInstrumentModal')
        },
        onDelete(selectedInstrument){
            this.selectedInstrument = selectedInstrument;
            this.$bvModal.show('deleteInstrumentModal')
        }
    },
    created(){
        this.getAll(
        )
    }
}
</script>
<style scoped>
    table{
        background-color:#171b2e;
    }
    h1{
        color:#ebeef2;  
    }
    td{
        color:#ebeef2;
    }
    .bgd{
      background-color:#171b2e;
    }
</style>