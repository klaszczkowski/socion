<template>
  <ion-page>
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Tab 2</ion-title>
        </ion-toolbar>
      </ion-header>
    
      <ExploreContainer name="Tab 1 page" />
  <ion-list>
    <ion-item>
      
      <ion-label>Pokémon Yellow</ion-label><ion-label>Pokémon Yellow</ion-label><ion-label>Pokémon Yellow</ion-label><ion-label>Pokémon Yellow</ion-label><ion-label>Pokémon Yellow</ion-label><ion-label>Pokémon Yellow</ion-label><ion-label>Pokémon Yellow</ion-label><ion-label>Pokémon Yellow</ion-label><ion-label>Pokémon Yellow</ion-label>
    </ion-item>
    <ion-item>
      <IonGrid>
        <IonRow>
          <IonCol>ion-col</IonCol>
          <IonCol>ion-col</IonCol>
          <IonCol>ion-col</IonCol>
          <IonCol>ion-col</IonCol>
        </IonRow>
      </IonGrid>

    </ion-item>
    <ion-item>
      <ion-label>The Legend of Zelda</ion-label>
    </ion-item>
    <ion-item>
      <ion-label>Pac-Man</ion-label>
    </ion-item>
    <ion-item>
      <ion-label>Super Mario World</ion-label>
    </ion-item>
  </ion-list>

  <!-- List of Input Items -->
  <ion-list>
    <ion-item>
      <ion-label>Input</ion-label>
      <ion-input></ion-input>
    </ion-item>
    <ion-item>
      <ion-label>Toggle</ion-label>
      <ion-toggle slot="end"></ion-toggle>
    </ion-item>
    <ion-item>
      <ion-label>Radio</ion-label>
      <ion-radio slot="end"></ion-radio>
    </ion-item>
    <ion-item>
      <ion-label>Checkbox</ion-label>
      <ion-checkbox slot="start"></ion-checkbox>
    </ion-item>
  </ion-list>

  <!-- List of Sliding Items -->
  <ion-list>
    <ion-item-sliding>
      <ion-item>
        <ion-label>Item</ion-label>
      </ion-item>
      <ion-item-options side="end">
        <ion-item-option @click="unread(item)">Unread</ion-item-option>
      </ion-item-options>
    </ion-item-sliding>

    <ion-item-sliding>
      <ion-item>
        <ion-label>Item</ion-label>
      </ion-item>
      <ion-item-options side="end">
        <ion-item-option @click="unread(item)">Unread</ion-item-option>
      </ion-item-options>
    </ion-item-sliding>
  </ion-list>

    </ion-content>
  </ion-page>
</template>

<script>
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent } from '@ionic/vue';
import ExploreContainer from '@/components/ExploreContainer.vue';

export default {
  name: 'Tab2',
  components: { ExploreContainer, IonHeader, IonToolbar, IonTitle, IonContent, IonPage },
  methods: {},
  data: () => {


    return {};
  }
}
</script>

<style scoped>
table {
  font-size: 10px;
}
table td {
    padding: 3px;
  }

  .three .three2, span.three {
      color: magenta
    }
</style>