<template>
    <div>
        <v-card
            elevation="2"
            color="#F0F7F4"
        >
            <v-row style="padding: 10px 30px;">
                <v-col>
                    <h2>Senarai Pengguna</h2>
                </v-col>
                <v-col style="text-align: end;">
                    <v-btn
                        color="success"
                        @click="handleAdd()"
                    >
                        <v-icon>mdi-plus</v-icon>
                        <span>Tambah Pengguna</span>
                    </v-btn>
                </v-col>
            </v-row>
            <v-row justify="center">
                <v-col cols="11">
                    <v-card
                        style="padding: 5px"
                        elevation="0"
                        outlined
                    >
                        <v-data-table
                            :loading="isLoading"
                            loading-text="Loading..."
                            :headers="headers"
                            :items="items"
                            item-key="id"
                            show-select
                            :single-select="false"
                            v-model:select="selected"
                            color="#B3BFB8"
                        >
                            <template v-slot:item.actions="{item}">
                                <v-icon
                                    small
                                    class="mr-2"
                                    @click="handleView(item)"
                                >
                                    mdi-eye
                                </v-icon>
                                <v-icon
                                    small
                                    class="mr-2"
                                    @click="handleEdit(item)"
                                >
                                    mdi-pencil
                                </v-icon>
                                <v-icon
                                    small
                                    class="mr-2"
                                    @click="handleDelete(item)"
                                >
                                    mdi-delete
                                </v-icon>
                            </template>
                        </v-data-table>
                    </v-card>
                </v-col>
            </v-row>
        </v-card>
    </div>
</template>
<script>
export default{
    data(){
        return{
            isLoading: false,
            headers:[
                {
                    text: "",
                    align: "center",
                    sortable: false,
                    value: "selection",
                },
                {
                    text: "Nama",
                    value: "name",
                },
                {
                    text: "Jawatan",
                    value: "position",
                },
                {
                    text: "Syarikat/Unit",
                    value: "company",
                },
                {
                    text: "Status",
                    value: "status",
                },
                {
                    text: "Tindakan",
                    align: "center",
                    sortable: false,
                    value: "actions"
                }
            ],
            items:[ 
                { id: 1, name: "Super User", company: "IT Department", position: "IT", status: "Active"},
                { id: 2, name: "Item 2", permission: "Permission 2", action: "Action 2" },
            ],
            selected:[]
        }
    },
    methods:{
        handleAdd(){
            this.$emit("changePage", "form", null, false);
        },
        handleDelete(item){
            console.log(item);
        },
        handleEdit(item) {
            this.$emit("changePage", "form", item, false);
        },
        handleView(item) {
            this.$emit("changePage", "form", item, true);
        }
    }
}
</script>