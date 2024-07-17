<template>
    <v-container>
        <v-row>
            <v-col cols=12>
                <h1>Peranan</h1>
            </v-col>
            <v-col>
                <v-divider></v-divider>
            </v-col>
        </v-row>
        <v-row>
            <v-col cols="12">
                <roleTable/>
            </v-col>
        </v-row>
    </v-container>
</template>
<script>
import roleTable from "@/components/tables/role.vue";

export default {
    components: {
        roleTable
    },
}
</script>