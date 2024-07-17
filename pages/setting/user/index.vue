<template>
    <v-container>
        <v-row>
            <v-col cols=12>
                <h1>Pengguna</h1>
            </v-col>
            <v-col>
                <v-divider></v-divider>
            </v-col>
        </v-row>
        <v-row>
            <v-col cols="12">
                <div v-if="currentPage==='form'">
                    <userForm
                        @changePage="changePage"
                        :title = "title"
                        :data = "data"
                        :isDisabled = "isDisabled"
                    />
                </div>
                <div v-else>
                    <userTable
                        @changePage="changePage"
                    />
                </div>
            </v-col>
        </v-row>
    </v-container>
</template>
<script>
import userTable from "@/components/tables/user.vue";
import userForm from "@/components/forms/user.vue";

export default {
    components: {
        userTable,
        userForm
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
            this.title = item? (isDisabled? 'Maklumat Pengguna':`Kemaskini Maklumat Pengguna`) : 'Tambah Pengguna';
            this.data = item;
            this.isDisabled = isDisabled;
        }
    },
}
</script>