<template>
    <v-container>
        <v-row align="center">
            <v-col class="d-flex" cols="12" sm="6">
                <v-select
                    :items="dProvice"
                    label="Province"
                    v-model="selectProvice"
                ></v-select>
            </v-col>

            <v-col class="d-flex" cols="12" sm="6">
                <v-select
                    :items="filterDistrict"
                    label="District"
                    v-model="selectDistrict"
                ></v-select>
            </v-col>

            <v-col class="d-flex" cols="12" sm="6">
                <v-select
                    :items="filterSubDistrict"
                    label="SubDistrict"
                    v-model="selectSubDistrict"
                ></v-select>
            </v-col>
        </v-row>
        <p>Provice: {{ selectProvice }}</p>
        <p>District: {{ selectDistrict }}</p>
        <p>SubDistrict: {{ selectSubDistrict }}</p>
    </v-container>
</template>

<script>
import db from "../assets/db.json";
export default {
    data() {
        return {
            data: db,
            dProvice: [],
            dDistrict: [],
            selectProvice: "",
            selectDistrict: "",
            selectSubDistrict: "",
        };
    },
    methods: {
        loadProvince() {
            this.dProvice = [...new Set(this.data.map((x) => x.ProvinceThai))]
            // this.dProvice = [...new Set(this.data.map((x) => x.ProvinceEng))]
        },
    },
    mounted() {
        this.loadProvince();
    },
    computed: {
        loadDistrict() {
            return this.data.filter((m) => {
                return m.ProvinceThai == this.selectProvice
                // return m.ProvinceEng == this.selectProvice
            });
        },
        filterDistrict() {
            return [...new Set(this.loadDistrict.map((x) => x.DistrictThai))]
            // return [...new Set(this.loadDistrict.map((x) => x.DistrictEng))]
        },
        loadSubDistrict() {
            return this.data.filter((m) => {
                return m.DistrictThai == this.selectDistrict
                // return m.DistrictEng == this.selectDistrict
            });
        },
        filterSubDistrict() {
            return [...new Set(this.loadSubDistrict.map((x) => x.TambonThai))]
            // return [...new Set(this.loadSubDistrict.map((x) => x.TambonEng))]
        },
    },
};
</script>
    

<style>
</style>