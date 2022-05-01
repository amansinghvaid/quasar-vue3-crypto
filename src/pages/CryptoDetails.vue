<template>
    <q-page padding>
        <div v-if="showDetails">
            <crypto-header 
                :symbol="details.symbol" 
                :name="details.name" 
                :image="details.image"
            >/</crypto-header>
            <q-separator></q-separator>
            <crypto-social
                :facebookUsername="details.links.facebook_username"
                :twitterUsername="details.links.twitter_screen_name"
                :redditUsername="details.links.subreddit_url"
            ></crypto-social>

            <div class="row q-pt-lg">
                <div class="col">
                    <p  v-html="details.description.en"></p>
                </div>
            </div>
            <div class="row">
                <div class="col">
                    <h4>Exchanges</h4>
                </div>
            </div>
            <div class="row">
                <div 
                    v-for="(ticker, index) in userTicker" 
                    :key="index" 
                    class="col-md-4 col-sm-6 col-xs-12"
                >
                    <crypto-exchange-card
                        :ticker="ticker"
                        :changeInLast24Hours="details.price_change_24h"
                    ></crypto-exchange-card>
                </div>
            </div>
        </div>
    </q-page>
  
</template>
<script>
import { ref, computed, reactive, onBeforeMount, getCurrentInstance } from 'vue'
import { useRoute } from 'vue-router'

import CryptoDetailsHeader from '../components/CryptoDetailsHeader.vue'
import CryptoDetailsSocialLinks from '../components/CryptoDetailsSocialLink.vue'
import CryptoExchangeCard from '../components/CryptoExchangeCard.vue'

export default {
    components: {
        'crypto-header': CryptoDetailsHeader,
        'crypto-social': CryptoDetailsSocialLinks,
        'crypto-exchange-card': CryptoExchangeCard
    },
    setup(){
        var showDetails = ref(false)
        const app = getCurrentInstance()
        const $api = app.appContext.config.globalProperties.$api
        const route = useRoute();
        var details = reactive({});
        var userTicker = computed(() => {
            return details.tickers.filter(ticker => ticker.target == 'USD')
        })
        onBeforeMount(async () => {
            const id =  route.params.id
            if(!id) {
                alert('Id not available')
                return
            }
            try{
                const res = await $api.get(`coins/${id}`);
                if(res.status === 200){
                    Object.assign(details, res.data);
                    showDetails.value = true
                } else{
                    alert('Some error occured.3')
                }
            }catch(err){
                console.log('Error', err)
                alert('Some error occured.4')
            }
        })

        return {
            details,
            showDetails,
            userTicker
        }
    }
}
</script>