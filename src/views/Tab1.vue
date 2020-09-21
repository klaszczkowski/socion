<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Tab 1</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Tab 1</ion-title>
        </ion-toolbar>
      </ion-header>
    
      <ExploreContainer name="Tab 1 page" />

      <table>
        <thead>
          <tr>
            <td v-for="type in types" :key="type.id">
              {{type.socionicsName}}
            </td>
          </tr>

        </thead>

        <tbody>
          <tr>
            <td v-for="type in types" :key="type.id">
              <!-- <button :click="buildDychotomies()">btn</button> -->
            </td>
          </tr>

        </tbody>

        <tfoot></tfoot>
      </table>
    </ion-content>
  </ion-page>
</template>

<script>
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent } from '@ionic/vue';
import ExploreContainer from '@/components/ExploreContainer.vue';

export default  {
  name: 'Tab1',
  components: { ExploreContainer, IonHeader, IonToolbar, IonTitle, IonContent, IonPage },
  methods: {
    buildDychotomies() {
      console.log(this.types);
    }
  },
  initialize() {
    this.buildDychotomies();
  },
  data: () => {
  const types = [
    {
      id: '0',
      socionicsName: 'sei',
      introverted: true,
      sensing: true,
      feeling: true,
      rational: false
    },
    {
      id: '1',
      socionicsName: 'ile',
      introverted: false,
      sensing: false,
      feeling: false,
      rational: false
    },
    {
      id: '2',
      socionicsName: 'lii',
      introverted: true,
      sensing: false,
      feeling: false,
      rational: true
    },
    {
      id: '3',
      socionicsName: 'ese',
      introverted: false,
      sensing: true,
      feeling: true,
      rational: true
    },
    {
      id: '4',
      socionicsName: 'lsi',
      introverted: true,
      sensing: true,
      feeling: false,
      rational: true
    },
    {
      id: '5',
      socionicsName: 'eie',
      introverted: false,
      sensing: false,
      feeling: true,
      rational: true
    },
    {
      id: '6',
      socionicsName: 'iei',
      introverted: true,
      sensing: false,
      feeling: true,
      rational: false
    },
    {
      id: '7',
      socionicsName: 'sle',
      introverted: false,
      sensing: true,
      feeling: false,
      rational: false
    },
    {
      id: '8',
      socionicsName: 'ili',
      introverted: true,
      sensing: false,
      feeling: false,
      rational: false
    },
    {
      id: '9',
      socionicsName: 'see',
      introverted: false,
      sensing: true,
      feeling: true,
      rational: false
    },
    {
      id: '10',
      socionicsName: 'esi',
      introverted: true,
      sensing: true,
      feeling: true,
      rational: true
    },
    {
      id: '11',
      socionicsName: 'lie',
      introverted: false,
      sensing: false,
      feeling: false,
      rational: true
    },
    {
      id: '12',
      socionicsName: 'lse',
      introverted: false,
      sensing: true,
      feeling: false,
      rational: true
    },
    {
      id: '13',
      socionicsName: 'eii',
      introverted: true,
      sensing: false,
      feeling: true,
      rational: true
    },
    {
      id: '14',
      socionicsName: 'iee',
      introverted: false,
      sensing: false,
      feeling: true,
      rational: false
    },
    {
      id: '15',
      socionicsName: 'sli',
      introverted: true,
      sensing: true,
      feeling: false,
      rational: false
    }
  ];

  const dichotomies = [
    {
      id: 'E',
      valid: 'Extrovert',
      null: 'Introvert'
    },
    {
      id: 'N',
      valid: 'Intuitive',
      null: 'Sensory'
    },
    {
      id: 'T',
      valid: 'Logical',
      null: 'Ethical'
    },
    {
      id: 'P',
      valid: 'Irrational',
      null: 'Rational'
    },
    {
      id: 'EN',
      valid: 'Carefree',
      null: 'Farsighted'
    },
    {
      id: 'ET',
      valid: 'Yielding',
      null: 'Obstinate'
    },
    {
      id: 'EP',
      valid: 'Static',
      null: 'Dynamic'
    },
    {
      id: 'NT',
      valid: 'Democratic',
      null: 'Aristocratic'
    },
    {
      id: 'NP',
      valid: 'Tactical',
      null: 'Strategic'
    },
    {
      id: 'TP',
      valid: 'Constructive',
      null: 'Emotive'
    },
    {
      id: 'ENT',
      valid: 'Positivist',
      null: 'Negativist'
    },
    {
      id: 'ENP',
      valid: 'Judicious',
      null: 'Decisive'
    },
    {
      id: 'ETP',
      valid: 'Merry',
      null: 'Serious'
    },
    {
      id: 'NTP',
      valid: 'Process',
      null: 'Results'
    },
    {
      id: 'ENTP',
      valid: 'Asking',
      null: 'Declaring'
    }
  ]

    return {types};
  }
}
</script>