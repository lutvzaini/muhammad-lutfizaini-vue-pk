<template>
    <div class="row">
        <div class="col-md-14">
            <ul class="list-group">
                <li
                    v-for="(fakta, index) in faktaKucing"
                    :key="index"
                    class="list-group-item list-group-item-warning"
                >
                    {{ index + 1 }}. {{ fakta.text }}
                </li>
            </ul>
        </div>
        <div class="row mt-4">
            <div class="col-md-14 text-center">
                <button @click="tampilkanLebihBanyakFakta" class="btn btn-md btn-warning">
                    {{ fetchingFakta ? "..." : "Tampilkan lebih banyak" }}
                </button>
            </div>
        </div>
    </div>
</template>
<script>
import { defineComponent } from "vue";
import axios from "axios";
export default defineComponent({
    name: "FaktaKucing",
    data() {
        return {
            faktaKucing: [],
            fetchingFakta: false,
        };
    },
    methods: {
        async fetchfaktaKucing() {
            const faktaKucingResponse = await axios.get(
                "https://cat-fact.herokuapp.com/facts/"
            );
            this.faktaKucing = faktaKucingResponse.data;
        },
        async tampilkanLebihBanyakFakta() {
            this.fetchingFakta = true;
            const faktaKucingResponse = await axios.get(
                "https://cat-fact.herokuapp.com/facts/"
            );
            this.faktaKucing.push(...(faktaKucingResponse.data || []));

            this.fetchingFakta = false;
        },
    },
    async mounted() {
        await this.fetchfaktaKucing();
    },
});
</script>

<style>
@media (min-width: 1024px) {
    .about {
        min-height: 100vh;
        display: flex;
        align-items: center;
    }
}
</style>
