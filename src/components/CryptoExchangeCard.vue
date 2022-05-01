<template>
    <q-card class="q-ma-md q-pa-sm">
        <q-card-section>
            <div class="text-h4">
                {{ ticker.market.name }}
                <!-- {{ ticker}} -->
            </div>
            <div class="text-h6">
                Trust: <q-avatar size="sm" :color="ticker.trust_score"></q-avatar>
            </div>
        </q-card-section>
        <q-separator></q-separator>
        <q-card-section>
            <div class="column flex flex-center">
                <div class="text-h4">
                    <q-icon 
                        :name="changeInLast24Hours > 0 ? 'trending_up': 'trending_down'"
                        :color="changeInLast24Hours > 0 ? 'green': 'red'"
                        size="24px"
                    ></q-icon>
                    ${{ ticker.last }}
                </div>
                <div class="text-h5 q-pt-md">
                    Volume: {{ ticker.volume.toFixed(2)}}
                </div>
            </div>
        </q-card-section>
        <q-card-actions>
            <q-btn
                type="a"
                color="primary"
                size="lg"
                :href="ticker.trade_url"
                target="_blank"
                flat
            >Trade</q-btn>
        </q-card-actions>
    </q-card>
</template>
<script>
import { defineComponent } from 'vue'
export default defineComponent({
    name: 'CryptoExchangeCard',
    props: {
        ticker: {
            type: Object,
            required: true
        },
        changeInLast24Hours: {
            type: Number,
            required: true
        }
    }
})
</script>