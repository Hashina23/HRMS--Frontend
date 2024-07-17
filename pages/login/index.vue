<template>
    <v-container style="padding: 5% 50px">
        <v-card
            height="600"
            shaped
            elevation="12"
        >
            <v-row style="height: 100%;">
                <v-col cols="8">
                    <v-img 
                        src="/login-bg.jpg"
                        contain
                        height="550"
                        width="800"
                        class="mx-auto"
                    />
                    <div style="opacity: 10%; margin-left: 20px; ">
                        <a href="https://www.freepik.com/free-vector/human-resources-concept-illustration_82454849.htm#fromView=search&page=1&position=3&uuid=c994dc3c-5eb3-4f9f-bf1b-2e71f01bf013">Image by storyset on Freepik</a>
                    </div>
                </v-col>
                <v-divider 
                    vertical 
                />
                <v-col>
                    <v-row style="height: 25%;">
                        <v-col style="align-content: center; text-align: center;">
                            <h1>
                                <span>
                                    HRMS
                                </span>
                            </h1>
                        </v-col>
                    </v-row>
                    <v-row>
                        <v-col>
                            <div class="form-container">
                                <h2 style="margin-bottom: 20px;">
                                    <span>Login</span>
                                </h2>
                                <v-form>
                                    <v-row 
                                        dense
                                        style="place-content: center;"
                                    >
                                        <v-col cols="12">
                                            <v-text-field
                                                v-model="username"
                                                label="Username"
                                                required
                                                outlined
                                            />
                                        </v-col>
                                        <v-col cols="12">
                                            <v-text-field
                                                v-model="password"
                                                label="Password"
                                                type="password"
                                                required
                                                outlined
                                            />
                                        </v-col>
                                        <v-col cols="12">
                                            <v-btn
                                                block
                                                color="primary"
                                                @click="login"
                                            >
                                                Login
                                            </v-btn>
                                        </v-col>
                                    </v-row>
                                </v-form>
                            </div>
                        </v-col>
                    </v-row>
                </v-col>
            </v-row>
        </v-card>
    </v-container>
</template>
<style>
.form-container{
    padding: 15px;
    padding-right: 20px;
}
</style>
<script>
export default{
    layout: 'empty',
    data(){
        return{
            username: '',
            password: ''
        }
    },
    methods:{
        login(){
            console.log('login as:', this.username, this.password);
            this.$router.push({name: 'dashboard'});
        }
    }
}
</script>