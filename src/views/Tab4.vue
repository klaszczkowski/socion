<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Tab 44</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Tab 4</ion-title>
        </ion-toolbar>
      </ion-header>

      <button v-on:click="callbapiBTCUSDT">
        c BTCUSDT
      </button>

      <br>

      <button v-on:click="buyCrypto">
        c btc usdt
      </button>

      <button @click="greet">Greet</button>
      
      <ExploreContainer name="Tab 4 page" />
    </ion-content>
  </ion-page>
</template>

<script>
// import axios from 'axios';
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent } from '@ionic/vue';
import ExploreContainer from '@/components/ExploreContainer.vue';
import crypto from 'crypto';

export default  {
  name: 'Tab4',
  components: { ExploreContainer, IonHeader, IonToolbar, IonTitle, IonContent, IonPage },
  data() {
    return {
      name: 'Vue.js',
      endpoint: 'https://api.binance.com'
    }
  },
  methods: {
    callbapiBTCUSDT() {
      const burl = "https://api.binance.com";

      let query = '/api/v1/ticker/24hr';
          
      query += '?symbol=BTCUSDT';

      const url = burl + query;
          
      const ourRequest = new XMLHttpRequest();

      ourRequest.open('GET',url,true);
      ourRequest.onload = function(){
          console.log(ourRequest.responseText);
      }
      ourRequest.send();  
      // axios
      //  .get(this.endpoint)
      //  .then(response => (this.info = response))
    },
    buyCrypto() {
      //Global Modules
      //Installed Modules

      const burl = "https://api.binance.com";
      const endPoint = "/api/v3/order";
      const dataQueryString = "symbol=BTCUSDT&side=BUY&type=LIMIT&timeInForce=GTC&quantity=0.001&price=15300&recvWindow=20000&timestamp=" + Date.now();

      const keys = {
          "akey" : 'tZjvAxGtkqj28rBViHDTnAsjE4IiBfqRnqYLlKUldHRwmQk7c7VxcQPUJ9OmGFpU',
          "skey" : 'sbdMXsWV2Ppm8lH1armEBrTilPXwnV8elMzrTpIG70bRRtvny3nVBhypnsYXZOUn'
      }

      const signature = crypto.createHmac('sha256',keys['skey']).update(dataQueryString).digest('hex');

      const url = burl + endPoint + '?' + dataQueryString + '&signature=' + signature;

      const ourRequest = new XMLHttpRequest();

      ourRequest.open('POST',url,true);
      ourRequest.setRequestHeader('X-MBX-APIKEY', keys['akey']);

      ourRequest.onload = function(){
          console.log(ourRequest.responseText);
      }
      ourRequest.send();
    },
    greet(event) {
      // `this` inside methods points to the current active instance
      alert('Hello ' + this.name + '!')
      // `event` is the native DOM event
      if (event) {
        alert(event.target.tagName)
      }
    }
  }
}
</script>