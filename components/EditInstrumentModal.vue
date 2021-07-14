<template>
    <div>
        <b-modal id="editInstrumentModal" title="Instrument Entry" ok-title="Save Instrument" @ok="onSubmit">
            <form action="#">
                <b-form-group label="Name" label-for="name">
                    <b-form-input id="name" v-model="instrument.name" trim></b-form-input>
                </b-form-group>
                
                <b-form-group label="Type" label-for="type">
                    <b-form-select  v-model="instrument.type" :options="types" trim></b-form-select>
                </b-form-group>

                <b-form-group label="Definition" label-for="definition">
                    <b-form-input id="definition" v-model="instrument.definition" trim></b-form-input>
                </b-form-group>

                <b-form-group label="Price" label-for="price">
                    <b-form-input id="price" v-model="instrument.price" trim></b-form-input>
                </b-form-group>

                <b-form-group label="Date Acquired" label-for="date acquired">
                    <b-form-input id="acquired_on" type="date" v-model="instrument.acquired_on" trim></b-form-input>
                </b-form-group>

                <b-form-group label="Range" label-for="range">
                    <b-form-select  v-model="instrument.range" :options="ranges" trim></b-form-select>
                </b-form-group>

            </form>
        </b-modal>
    </div>
</template>

<script>
export default {
    props: {
        instrument: {}
    },
    data(){
        return {
                types:[
                {value: 'woodwind',text: 'woodwind'},
                {value: ' brass',text: 'brass'},
                {value: ' percussion',text: 'percussion'},
                {value: ' string',text: 'string'},
                {value: ' keyboard',text: 'keyboard'},
            ],
            ranges:[
                {value: 'Soprano',text:'Soprano'},
                {value: 'Tenor',text:'Tenor'},
                {value: 'Alto',text:'Alto'},
            ],
        }
    },
    methods: {
        async onSubmit(){
            this.$axios.put('/api/instruments/' + this.instrument.id,this.instrument)
            .then((res)=>{
                if(res.status==202){
                    alert('Update successfully!!!')
                }
            })
            .catch((err)=>{
                alert(err.message)
            })
        }
    }
}
</script>