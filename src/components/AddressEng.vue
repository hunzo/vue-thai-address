<template>
    <v-container>
        <v-card elevation="10">
            <v-card-text class="indigo white--text">
                Select Address
            </v-card-text>
            <v-card-text>
                <v-row align="center">
                    <v-col class="d-flex" cols="12" sm="6">
                        <v-select
                            :items="dProvice"
                            label="Province"
                            v-model="selectProvice"
                            outlined
                            dense
                        ></v-select>
                    </v-col>

                    <v-col class="d-flex" cols="12" sm="6">
                        <v-select
                            :items="filterDistrict"
                            label="District"
                            v-model="selectDistrict"
                            outlined
                            dense
                        ></v-select>
                    </v-col>

                    <v-col class="d-flex" cols="12" sm="6">
                        <v-select
                            :items="filterSubDistrict"
                            label="SubDistrict"
                            v-model="selectSubDistrict"
                            outlined
                            dense
                        ></v-select>
                    </v-col>

                    <v-col class="d-flex" cols="12" sm="6">
                        <v-text-field
                            label="ZipCode"
                            :placeholder="filterZipCode"
                            outlined
                            dense
                            readonly
                        ></v-text-field>
                    </v-col>
                </v-row>
                <p>Provice: {{ selectProvice }}</p>
                <p>District: {{ selectDistrict }}</p>
                <p>SubDistrict: {{ selectSubDistrict }}</p>
                <p>ZipCode: {{ filterZipCode[0] }}</p>
            </v-card-text>
        </v-card>
    </v-container>
</template>

<script>
import db from "../assets/db.json"
export default {
    data() {
        return {
            data: db,
            dProvice: [],
            dDistrict: [],
            selectProvice: "",
            selectDistrict: "",
            selectSubDistrict: "",
        }
    },
    methods: {
        loadProvince() {
            // this.dProvice = [...new Set(this.data.map((x) => x.ProvinceThai))]
            this.dProvice = [...new Set(this.data.map((x) => x.ProvinceEng))]
        },
    },
    mounted() {
        this.loadProvince()
    },
    computed: {
        loadDistrict() {
            return this.data.filter((m) => {
                // return m.ProvinceThai == this.selectProvice
                return m.ProvinceEng == this.selectProvice
            })
        },
        filterDistrict() {
            // return [...new Set(this.loadDistrict.map((x) => x.DistrictThai))]
            return [...new Set(this.loadDistrict.map((x) => x.DistrictEng))]
        },
        loadSubDistrict() {
            return this.data.filter((m) => {
                // return m.DistrictThai == this.selectDistrict
                return m.DistrictEng == this.selectDistrict
            })
        },
        filterSubDistrict() {
            // return [...new Set(this.loadSubDistrict.map((x) => x.TambonThai))]
            return [...new Set(this.loadSubDistrict.map((x) => x.TambonEng))]
        },
        loadZipCode() {
            return this.data.filter((m) => {
                return m.TambonEng == this.selectSubDistrict
            })
        },
        filterZipCode() {
            return [...new Set(this.loadZipCode.map((x) => x.PostCodeMain))]
        }
    },
};
</script>
    

<style>
</style>