<template>
    <div class="container xl:px-56 flex justify-center">
        <div class="bg-gray-700 p-2 mt-3 rounded">
            <VPagination
                v-model="page"
                :pages="99"
                :range-size="1"
                active-color="#FFF"
                @update:modelValue="updateHandler; this.$router.replace({name: 'release.page', params:{ page: this.page}})"
            />
        </div>
    </div>
</template>

<script>
import VPagination from "@hennge/vue3-pagination";
import "@hennge/vue3-pagination/dist/vue3-pagination.css";

export default {
    data() {
        return {
            page: 1
        }
    },
    components: {
        VPagination
    },
    methods: {
        updateHandler(value) {
            this.page = value
        }
    }
}
</script>
