<template>
    <v-container>
        <v-card elevation="10">
            <v-card-title class="info white--text"> เลือกที่อยู่ </v-card-title>
            <v-card-text>
                <v-row align="center">
                    <v-col class="d-flex" cols="12" sm="6">
                        <v-select
                            :items="dProvice"
                            label="จังหวัด"
                            v-model="selectProvice"
                            outlined
                            dense
                        ></v-select>
                    </v-col>

                    <v-col class="d-flex" cols="12" sm="6">
                        <v-select
                            :items="filterDistrict"
                            label="อำเภอ"
                            v-model="selectDistrict"
                            outlined
                            dense
                        ></v-select>
                    </v-col>

                    <v-col class="d-flex" cols="12" sm="6">
                        <v-select
                            :items="filterSubDistrict"
                            label="ตำบล"
                            v-model="selectSubDistrict"
                            outlined
                            dense
                        ></v-select>
                    </v-col>

                    <v-col class="d-flex" cols="12" sm="6">
                        <v-text-field
                            label="รหัสไปรษณีย์"
                            :placeholder="filterZipCode"
                            outlined
                            dense
                            readonly
                        ></v-text-field>
                    </v-col>
                </v-row>
                <p>จังหวัด: {{ selectProvice }}</p>
                <p>อำเภอ: {{ selectDistrict }}</p>
                <p>ตำบล: {{ selectSubDistrict }}</p>
                <p>รหัสไปรษณีย์: {{ filterZipCode[0] }}</p>
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
            this.dProvice = [...new Set(this.data.map((x) => x.ProvinceThai))]
            // this.dProvice = [...new Set(this.data.map((x) => x.ProvinceEng))]
        },
    },
    mounted() {
        this.loadProvince()
    },
    computed: {
        loadDistrict() {
            return this.data.filter((m) => {
                return m.ProvinceThai == this.selectProvice
                // return m.ProvinceEng == this.selectProvice
            })
        },
        filterDistrict() {
            return [...new Set(this.loadDistrict.map((x) => x.DistrictThai))]
            // return [...new Set(this.loadDistrict.map((x) => x.DistrictEng))]
        },
        loadSubDistrict() {
            return this.data.filter((m) => {
                return m.DistrictThai == this.selectDistrict
                // return m.DistrictEng == this.selectDistrict
            })
        },
        filterSubDistrict() {
            return [...new Set(this.loadSubDistrict.map((x) => x.TambonThai))]
            // return [...new Set(this.loadSubDistrict.map((x) => x.TambonEng))]
        },
        loadZipCode() {
            return this.data.filter((m) => {
                return m.TambonThai == this.selectSubDistrict
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