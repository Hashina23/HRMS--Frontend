<template>
    <div>
        <v-card
            color="#F0F7F4"
        >   
            <v-row style="padding: 10px 30px">
                <v-col>
                    <h2>{{ title }}</h2>
                </v-col>
                <div v-if="!isDisabled">
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
                </div>
                <div v-else>
                    <v-col style="text-align: end;">
                        <v-btn
                            color="success"
                            @click="onCancel"
                        >
                            <v-icon>mdi-arrow-left</v-icon>
                            <span style="padding-left: 5px;">Balik</span>
                        </v-btn>
                    </v-col>
                </div>
            </v-row>
        </v-card>
        <div style="height: 30px;"/>
        <v-form ref="form">
            <v-card>
                <v-row style="padding: 10px 40px">
                    <v-col cols="12">
                        <h3>Maklumat Syarikat</h3>
                    </v-col>
                </v-row>
                <v-row style="padding-left: 45px;">
                        <v-col cols="3" >
                            <v-subheader 
                                class="subheader-text"
                            >
                                Nama :
                            </v-subheader>
                        </v-col>
                        <v-col cols="4">
                            <v-text-field 
                                outlined    
                                dense
                                v-model="name"
                                :rules="nameRules"
                                :disabled="isDisabled"
                            ></v-text-field>
                        </v-col>
                </v-row>
                <v-row style="padding-left: 45px;">
                        <v-col cols="3" >
                            <v-subheader 
                                class="subheader-text"
                            >
                                Email :
                            </v-subheader>
                        </v-col>
                        <v-col cols="4">
                            <v-text-field 
                                outlined    
                                dense
                                v-model="email"
                                :rules="emailRules"
                                :disabled="isDisabled"
                            ></v-text-field>
                        </v-col>
                </v-row>
                <v-row style="padding-left: 45px;">
                        <v-col cols="3" >
                            <v-subheader 
                                class="subheader-text"
                            >
                                Nombor Telefon :
                            </v-subheader>
                        </v-col>
                        <v-col cols="4">
                            <v-text-field 
                                outlined    
                                dense
                                v-model="phoneNo"
                                :rules="phoneNoRules"
                                :disabled="isDisabled"
                            ></v-text-field>
                        </v-col>
                </v-row>
                <v-row style="padding-left: 45px;">
                        <v-col cols="3" >
                            <v-subheader 
                                class="subheader-text"
                            >
                                Alamat :
                            </v-subheader>
                        </v-col>
                        <v-col cols="4">
                            <v-textarea
                                outlined
                                no-resize
                                v-model="address"
                                :rules="addressRules"
                                :disabled="isDisabled"
                            />
                        </v-col>
                </v-row>
            </v-card>
        </v-form>
    </div>
</template>
<style scoped>
.subheader-text{
    font-size: large;
}
</style>
<script>
export default{
    props:{
        title:{
            type: String,
            required: true,
        },
        data:{
            type: Object,
            required: false,
        },
        isDisabled:{
            type: Boolean,
            default: true,
        }
    },
    data(){
        return{
            name: null,
            email: null,
            phoneNo: null,
            address: null,

            //rules
            nameRules: [
                v => !!v || 'Nama diperlukan',
            ],
            emailRules: [
                v => !!v || 'Email diperlukan',
                v => /.+@.+\..+/.test(v) || 'Email tidak sah',
            ],
            phoneNoRules: [
                v => !!v || 'Nombor telefon diperlukan',
                v => /^\d{10,15}$/.test(v) || 'Nombor telefon tidak sah',
            ],
            addressRules: [
                v => !!v || 'Alamat diperlukan',
                // v => (v && v.length <= 100) || 'Alamat mesti kurang dari 100 aksara',
            ],
        }
    },
    methods: {
        fetchUserInformation(){
            //check if data is available
            //if available, then fetch from backend
            if(this.data == null){
                console.log("here");
            }else{
                this.name = this.data.name;
                console.log(this.data);
            }
        },
        onCancel(){
            this.$emit('changePage', '');
        },
        onSubmit(){
            if(this.$refs.form.validate()){
                var form = {
                    name: this.name,
                    email: this.email,
                    phoneNo: this.phoneNo,
                    address: this.address,
                };
                if(!this.data){
                    //Add new role
                    console.log(form);
                }else{
                    //Update existing role
                    Object.assign(form, {id: this.data.id});
                    console.log(form);
                }
            }
        }
    },
    mounted(){
        this.fetchUserInformation();
    }
}
</script>
