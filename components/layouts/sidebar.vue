<template>
    <div>
        <v-navigation-drawer v-model="drawer" :mini-variant.sync="mini" permanent color="#342e37" app>
            <v-list-item class="side-icon px-2">
                <v-btn icon @click="trigger">
                    <v-icon class="text-color">mdi-menu</v-icon>
                </v-btn>
            </v-list-item>
            <v-list-item class="px-2">
                <div>&nbsp;</div>
                <v-list-item-title style="text-align: center;">
                    <h1 class="text-color">HRMS</h1>
                </v-list-item-title>
            </v-list-item>
            <v-list-item class="px-2">
                <div>&nbsp;</div>
                <v-divider style="background-color: #4a414e;"></v-divider>
            </v-list-item>
            <v-list>
                <v-list-item-group>
                    <div v-for="(item, index) in items" :key="index" v-if="!item.subItems">
                        <v-list-item :to="item.to" class="text-color">
                            <v-list-item-icon>
                                <v-icon class="text-color">{{ item.icon }}</v-icon>
                            </v-list-item-icon>
                            <v-list-item-title class="text-color">{{ item.title }}</v-list-item-title>
                        </v-list-item>
                    </div>
                    <div v-else>
                        <v-list-group no-action>
                            <template slot="activator">
                                <v-list-item-icon>
                                    <v-icon class="text-color">{{ item.icon }}</v-icon>
                                </v-list-item-icon>
                                <v-list-item-title class="text-color">{{ item.title }}</v-list-item-title>
                            </template>
                            <v-icon class="text-color" slot="appendIcon">mdi-chevron-down</v-icon>
                            <v-list-item v-for="(subItem, index) in item.subItems" :key="index" :to="subItem.to"
                                class="text-color" style="padding-left: 32px;">
                                <v-list-item-icon>
                                    <v-icon class="text-color">{{ subItem.icon }}</v-icon>
                                </v-list-item-icon>
                                <v-list-item-title class="text-color">
                                    {{ subItem.title }}
                                </v-list-item-title>
                            </v-list-item>
                        </v-list-group>
                    </div>
                </v-list-item-group>
            </v-list>
            <v-list-item class="side-icon px-2 logout-button">
                <v-btn icon @click="logout">
                    <v-icon class="text-color">mdi-logout</v-icon>
                </v-btn>
            </v-list-item>
        </v-navigation-drawer>

    </div>
</template>

<style scoped>
.side-icon {
    padding: 0;
}

.logout-button {
    position: absolute;
    bottom: 0px;
}

.text-color {
    color: white !important;
}
</style>

<script>
export default {
    data() {
        return {
            drawer: true,
            mini: true,
            items: [
                {
                    title: "Laman Utama",
                    icon: "mdi-home",
                    to: "/dashboard",
                },
                {
                    title: "Tetapan",
                    icon: "mdi-cogs",
                    subItems: [
                        {
                            title: "Pengguna",
                            icon: "mdi-account",
                            to: "/setting/user",
                        },
                        {
                            title: "Jawatan",
                            icon: "mdi-account-badge",
                            to: "/setting/position",
                        },
                        {
                            title: "Syarikat/Unit",
                            icon: "mdi-office-building",
                            to: "/setting/company",
                        },
                        {
                            title: "Peranan",
                            icon: "mdi-account-cog",
                            to: "/setting/role",
                        },
                    ],
                }
            ],
        }
    },
    methods: {
        trigger() {
            this.mini = !this.mini;
        },
        logout() {
            this.$router.push('/login');
        }
    }
}
</script>
