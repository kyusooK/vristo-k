<template>
    <div>
        <BasePicker v-if="editMode" searchApiPath="ranks" searchParameterName="id"  idField="id" nameField="id" path="ranks" label="RankId" v-model="value" @selected="pick" :editMode="editMode" />
        <div v-else style="height:100%">
            <span>{{ value && value.name ? value.name : '' }}</span>
        </div>
    </div>

</template>

<script>
import BaseEntity from './base-ui/BaseEntity'

export default {
    name: 'RankId',
    mixins:[BaseEntity],
    components:{
    },
    data: () => ({
        path: 'ranks',
    }),
    props: {
    },
    watch: {
        value(val){
            this.value = val;
            this.change();
        },
    },
    async created(){
        if (this.value && this.value.id !== undefined) {
            this.value = await this.repository.findById(this.value.id)
        }
    },
    methods: {
        pick(val){
            this.value = val;
            this.change();
        },
    }
}
</script>

