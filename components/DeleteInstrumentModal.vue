<template>
    <div>
        <b-modal id="deleteInstrumentModal" title="Instrument Entry" ok-title="Delete Instrument" @ok="onDelete" ok-variant="danger">
            Are you sure about deleting this instrument? <br>
            {{instrument.name}} {{instrument.definition}}
        </b-modal>
    </div>
</template>
<script>
export default {
    props: {
        instrument: {}
    },
    methods: {
        async onDelete(){
            this.$axios.delete('/api/instruments/' + this.instrument.id)
            .then((res)=>{
                if(res.status==202){
                    alert('Instrument is deleted successfully')
                    this.$emit('onDeleted')
                }
            })
        }
    }
}
</script>