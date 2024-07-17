<template>
    <v-container>
        <v-row>
            <v-col cols=12>
                <h1>Jawatan</h1>
            </v-col>
            <v-col>
                <v-divider></v-divider>
            </v-col>
        </v-row>
        <v-row>
            <v-col cols="12">
                <div v-if="currentPage==='form'">
                    <positionForm
                        @changePage="changePage"
                        :title = "title"
                        :data = "data"
                        :isDisabled = "isDisabled"
                    />
                </div>
                <div v-else>
                    <positionTable
                        @changePage="changePage"
                    />
                </div>
            </v-col>
        </v-row>
    </v-container>
</template>
<script>
import positionTable from "@/components/tables/position.vue";
import positionForm from "@/components/forms/position.vue";

export default {
    components: {
        positionTable,
        positionForm
    },
    data() {
        return {
            currentPage: '',
            title: '',
            data: {},
            isDisabled: false,
        }
    },
    methods:{
        changePage(page, item, isDisabled) {
            this.currentPage = page;
            this.title = item? (isDisabled? 'Maklumat Jawatan':`Kemaskini Maklumat Jawatan`) : 'Tambah Jawatan';
            this.data = item;
            this.isDisabled = isDisabled;
        }
    },
}
</script>