<template>
    <div class="row">
        <div class="col flex flex-center">
            <q-img width="50px" :src="image.small"></q-img>
            <span class="text-h3 q-pt-md q-pb-md">
                {{ `${name} - ${symbol}`}}
            </span>
        </div>
    </div>
</template>
<script>
export default {
    props: {
        image: {
            type: Object,
            required: true
        },
        name: {
            type: String,
            required: true
        },
        symbol: {
            type: String,
            required: true
        },
    },
    setup(props) {

        return {

        }
    }
}
</script>