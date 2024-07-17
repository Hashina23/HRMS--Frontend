<template>
    <div>
        <v-card>   
            <v-row style="padding: 10px 30px">
                <v-col>
                    <h2>{{ title }}</h2>
                </v-col>
                <v-col style="text-align: end;">
                    <v-btn
                        color="success"
                        @click="onSubmit"
                    >
                        <v-icon>mdi-content-save</v-icon>
                        <span style="padding-left: 5px;">Simpan</span>
                    </v-btn>
                    <v-btn
                        color="error"
                        @click="onCancel"
                    >
                        <v-icon>mdi-close</v-icon>
                        <span style="padding-left: 5px;">Batal</span>
                    </v-btn>
                </v-col>
            </v-row>
            <v-row style="padding-left: 45px;">
                    <v-col cols="2" >
                        <v-subheader>Nama Peranan :</v-subheader>
                    </v-col>
                    <v-col cols="4">
                        <v-text-field 
                            outlined    
                            dense
                            v-model="roleName"
                        ></v-text-field>
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
                            :headers="headers"
                            :items="rolePermission"
                        >
                            <template v-slot:item.view="{item}">
                                <v-simple-checkbox
                                    v-model="item.view"
                                >
    
                                </v-simple-checkbox>
                            </template>
                            <template v-slot:item.edit="{item}">
                                <v-simple-checkbox
                                    v-model="item.edit"
                                >
    
                                </v-simple-checkbox>
                            </template>
                        </v-data-table>
                    </v-card>
                </v-col>
            </v-row>
        </v-card>
    </div>
</template>
<style scoped>

</style>
<script>
export default{
    props:{
        title:{
            type: String,
            required: true,
        },
        role:{
            type: Object,
            required: false,
        }
    },
    data(){
        return{
            roleName: null,
            headers:[
                {
                    text: '',
                    value: 'name'
                },
                {
                    text: 'View',
                    value: 'view',
                    sortable: false
                },
                {
                    text: 'Edit',
                    value: 'edit',
                    sortable: false
                }
            ],
            rolePermission:[
            // {
            //         name: 'User',
            //         view: false,
            //         edit: false
            //     },
            //     {
            //         name: 'Leave',
            //         view: false,
            //         edit: false
            //     },
            //     {
            //         name: 'Claim',
            //         view: false,
            //         edit: false
            //     },
            ],
        }
    },
    methods: {
        //fetch list of role from backend
        //mounted current permission from the backend if it exists
        fetchRolePermissions(){
            if(!this.role){
                var accessPanel = ['User', 'Leave', 'Claim'];

                accessPanel.forEach(panel => {
                    this.rolePermission.push({
                        name: panel,
                        view: false,
                        edit: false
                    });
                });
            }else{
                this.roleName= this.role.name;
            }
        },
        onCancel(){
            this.$router.push('/setting/role');
        },
        onSubmit(){
            var form = {
                name: this.roleName,
            }
            this.rolePermission.forEach(role => {
                form[role.name] = {
                    view: role.view,
                    edit: role.edit
                }
            });

            if(!this.role){
                //Add new role
                console.log(form);
            }else{
                //Update existing role
                Object.assign(form, {id: this.role.id});
                console.log(form);
            }
        }
    },
    mounted(){
        this.fetchRolePermissions(); 
    }
}
</script>
