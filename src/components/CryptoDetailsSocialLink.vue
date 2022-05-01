<template>
    <div class="row q-pt-lg">
        <div class="col flex flex-center">
            <q-btn
                v-if="facebookUsername"
                type="a"
                color="primary"
                class="q-mr-md"
                :href="`https://facebook.com/${facebookUsername}`"
                target="_blank"
            >
                <q-icon class="q-pr-sm" name="mdi-facebook"></q-icon> Facebook
            </q-btn>
            <q-btn
                v-if="twitterUsername"
                type="a"
                color="blue"
                class="q-mr-md"
                :href="`https://twitter.com/${twitterUsername}`"
                target="_blank"
            >
                 <q-icon class="q-pr-sm" name="mdi-twitter"></q-icon> Twitter
            </q-btn>
            <q-btn
                v-if="redditUsername"
                type="a"
                color="black"
                class="q-mr-md"
                :href="redditUsername"
                target="_blank"
            >
                 <q-icon class="q-pr-sm" name="mdi-reddit"></q-icon> Reddit
            </q-btn>
        </div>
    </div>
</template>
<script>
import { defineComponent} from 'vue'
export default defineComponent({
    name: 'CryptoDetailsSocialLinks',
    props: {
        facebookUsername: {
            type: String,
            required: true
        },
        twitterUsername: {
            type: String,
            required: true
        },
        redditUsername: {
            type: String,
            required: true
        }
    },
    setup() {

        return {

        }
    }
})
</script>