<template>
    <v-container>
        <v-row>
            <v-col cols=12>
                <h1>Syarikat/Unit</h1>
            </v-col>
            <v-col>
                <v-divider></v-divider>
            </v-col>
        </v-row>
        <v-row>
            <v-col cols="12">
                <div v-if="currentPage==='form'">
                    <companyForm
                        @changePage="changePage"
                        :title = "title"
                        :data = "data"
                        :isDisabled = "isDisabled"
                    />
                </div>
                <div v-else>
                    <companyTable
                        @changePage="changePage"
                    />
                </div>
            </v-col>
        </v-row>
    </v-container>
</template>
<script>
import companyTable from "@/components/tables/company.vue";
import companyForm from "@/components/forms/company.vue";

export default {
    components: {
        companyTable,
        companyForm
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
            this.title = item? (isDisabled? 'Maklumat Syarikat/Unit':`Kemaskini Maklumat Syarikat/Unit`) : 'Tambah Syarikat/Unit';
            this.data = item;
            this.isDisabled = isDisabled;
        }
    },
}
</script>