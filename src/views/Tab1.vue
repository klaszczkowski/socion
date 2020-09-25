<template>
  <ion-page>
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
            <td></td>

            <td v-for="type in types" :key="type.id">
              {{type.socionicsName}} / <span class="three">{{ type.dich4 }}</span>
            </td>
          </tr>

        </thead>

        <tbody>
          <tr :class="{'three': dichotomy.traits.length == 4}" v-for="dichotomy in dichotomies" :key="dichotomy.id">
            <td><span class="three2">{{ dichotomy.valid }}</span> / {{ dichotomy.null }} / {{ dichotomy.id }}</td>
            <td v-for="type in types" :key="type.id">
              {{ type.dichotomies[dichotomy.valid] }}
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

export default {
  name: 'Tab1',
  components: { ExploreContainer, IonHeader, IonToolbar, IonTitle, IonContent, IonPage },
  methods: {
    isTypeMatchDychotomy(socionicsName, dichotomyId) {
      let typeData;
      let dichotomyData;

      for (const type of this.types) {
        if (type.socionicsName == socionicsName) {
          typeData = type;
        }
      }

      for (const dichotomy of this.dichotomies) {
        if (dichotomy.id == dichotomyId) {
          dichotomyData = dichotomy;
        }
      }

      let toReturn;

      const traitsIndicatorsCount = dichotomyData.traits.length;

      if (traitsIndicatorsCount == 3) {
        const comparisonResults = [];
        let i;
        for (i = 0; i<traitsIndicatorsCount; i++) {
          if (typeData.traits[dichotomyData.traits[i]] == true) {
            comparisonResults.push(true);
          } else {
            comparisonResults.push(false);
          }
        }

        if (this.isAllComparisonResultsSame(comparisonResults) && comparisonResults[0] == true) {
          toReturn = true;
        } else if (this.isAllComparisonResultsSame(comparisonResults) && comparisonResults[0] == false) {
          toReturn = false;
        } else if (!this.isAllComparisonResultsSame(comparisonResults)) {
          toReturn = !this.isDoubleDichotomyTrue(dichotomyData.traits, typeData.traits);
        }

      } else if (traitsIndicatorsCount == 1) {
        toReturn = typeData.traits[dichotomyData.traits[0]] == true;
      } else if (traitsIndicatorsCount == 2) {
        const comparisonResults = [];
        let i;
        for (i = 0; i<traitsIndicatorsCount; i++) {
          if (typeData.traits[dichotomyData.traits[i]] == true) {
            comparisonResults.push(true);
          } else {
            comparisonResults.push(false);
          }
        }

        if (this.isAllComparisonResultsSame(comparisonResults)) {
          toReturn = true;
        }
      } else if (traitsIndicatorsCount == 4) {
        const comparisonResults = [];
        let i;
        for (i = 0; i<traitsIndicatorsCount; i++) {
          if (typeData.traits[dichotomyData.traits[i]] == true) {
            comparisonResults.push(true);
          } else {
            comparisonResults.push(false);
          }
        }

        if (this.isAllComparisonResultsSame(comparisonResults)) {
          toReturn = true;
        } else if (this.isDoubleDichotomyTrue(dichotomyData.traits, typeData.traits)) {
          toReturn = true;
        } else {
          toReturn = false;
        }
      }

      return toReturn;
    },
    isDoubleDichotomyTrue(dichotomyDataTraits, typeDataTraits) {
      const singleDichotomiesInTrueState = [];
      for (const trait of dichotomyDataTraits) {
        if (typeDataTraits[trait] == true) {
          singleDichotomiesInTrueState.push(trait)
        }
      }
      return singleDichotomiesInTrueState.length == 2;
    },
    isAllComparisonResultsSame(results) {
      const firstResult = results[0];
      return results.indexOf(!firstResult) == -1;
    },
    buildDychotomies() {
      this.types.forEach(type => {
        this.dichotomies.forEach(dichotomy => {
          if (this.isTypeMatchDychotomy(type.socionicsName, dichotomy.id)) {
            type.dichotomies[dichotomy.valid] = true;
          } else {
            type.dichotomies[dichotomy.valid] = false;
          }
        });
      });
    }
  },
  mounted() {
    this.buildDychotomies();
  },
  data: () => {
  const types = [
    {
      id: '0',
      socionicsName: 'sei',
      traits: {
        E: false,
        N: false,
        T: false,
        P: true
      },
      dichotomies: {},
      introverted: true,
      sensing: true,
      feeling: true,
      rational: false,
      dich3: 'negativist	judicious	subjectivist	process',
      dich2: 'carefree	yielding	dynamic	democratic	strategic	emotivist',
      dich4: 'declaring'
    },
    {
      id: '1',
      socionicsName: 'ile',
      traits: {
        E: true,
        N: true,
        T: true,
        P: true
      },
      dichotomies: {},
      introverted: false,
      sensing: false,
      feeling: false,
      rational: false,
      dich3: 'positivist	judicious	subjectivist	process',
      dich2: 'carefree	yielding	static	democratic	tactical	constructivist',
      dich4: 'asking'
    },
    {
      id: '2',
      socionicsName: 'lii',
      traits: {
        E: false,
        N: true,
        T: true,
        P: false
      },
      dichotomies: {},
      introverted: true,
      sensing: false,
      feeling: false,
      rational: true,
      dich3: 'negativist	judicious	subjectivist	result',
      dich2: 'farsighted	obstinate	static	democratic	strategic	emotivist',
      dich4: 'asking'
    },
    {
      id: '3',
      socionicsName: 'ese',
      traits: {
        E: true,
        N: false,
        T: false,
        P: false
      },
      dichotomies: {},
      introverted: false,
      sensing: true,
      feeling: true,
      rational: true,
      dich3: 'positivist	judicious	subjectivist	result',
      dich2: 'farsighted	obstinate	dynamic	democratic	tactical	constructivist',
      dich4: 'declaring'
    },
    {
      id: '4',
      socionicsName: 'lsi',
      traits: {
        E: false,
        N: false,
        T: true,
        P: false
      },
      dichotomies: {},
      introverted: true,
      sensing: true,
      feeling: false,
      rational: true,
      dich3: 'positivist	decisive	subjectivist	process',
      dich2: 'carefree	obstinate	static	aristocratic	tactical	emotivist',
      dich4: 'declaring'
    },
    {
      id: '5',
      socionicsName: 'eie',
      traits: {
        E: true,
        N: true,
        T: false,
        P: false
      },
      dichotomies: {},
      introverted: false,
      sensing: false,
      feeling: true,
      rational: true,
      dich3: 'negativist	decisive	subjectivist	process',
      dich2: 'carefree	obstinate	dynamic	aristocratic	strategic	constructivist',
      dich4: 'asking'
    },
    {
      id: '6',
      socionicsName: 'iei',
      traits: {
        E: false,
        N: true,
        T: false,
        P: true
      },
      dichotomies: {},
      introverted: true,
      sensing: false,
      feeling: true,
      rational: false,
      dich3: 'positivist	decisive	subjectivist	result',
      dich2: 'farsighted	yielding	dynamic	aristocratic	tactical	emotivist',
      dich4: 'asking'
    },
    {
      id: '7',
      socionicsName: 'sle',
      traits: {
        E: true,
        N: false,
        T: true,
        P: true
      },
      dichotomies: {},
      introverted: false,
      sensing: true,
      feeling: false,
      rational: false,
      dich3: 'negativist	decisive	subjectivist	result',
      dich2: 'farsighted	yielding	static	aristocratic	strategic	constructivist',
      dich4: 'declaring'
    },
    {
      id: '8',
      socionicsName: 'ili',
      traits: {
        E: false,
        N: true,
        T: true,
        P: true
      },
      dichotomies: {},
      introverted: true,
      sensing: false,
      feeling: false,
      rational: false,
      dich3: 'negativist	decisive	objectivist	process',
      dich2: 'farsighted	obstinate	dynamic	democratic	tactical	constructivist',
      dich4: 'declaring'
    },
    {
      id: '9',
      socionicsName: 'see',
      traits: {
        E: true,
        N: false,
        T: false,
        P: true
      },
      dichotomies: {},
      introverted: false,
      sensing: true,
      feeling: true,
      rational: false,
      dich3: 'positivist	decisive	objectivist	process',
      dich2: 'farsighted	obstinate	static	democratic	strategic	emotivist',
      dich4: 'asking'
    },
    {
      id: '10',
      socionicsName: 'esi',
      traits: {
        E: false,
        N: false,
        T: false,
        P: false
      },
      dichotomies: {},
      introverted: true,
      sensing: true,
      feeling: true,
      rational: true,
      dich3: 'negativist	decisive	objectivist	result',
      dich2: 'carefree	yielding	static	democratic	tactical	constructivist',
      dich4: 'asking'
    },
    {
      id: '11',
      socionicsName: 'lie',
      traits: {
        E: true,
        N: true,
        T: true,
        P: false
      },
      dichotomies: {},
      introverted: false,
      sensing: false,
      feeling: false,
      rational: true,
      dich3: 'positivist	decisive	objectivist	result',
      dich2: 'carefree	yielding	dynamic	democratic	strategic	emotivist',
      dich4: 'declaring'
    },
    {
      id: '12',
      socionicsName: 'lse',
      traits: {
        E: true,
        N: false,
        T: true,
        P: false
      },
      dichotomies: {},
      introverted: false,
      sensing: true,
      feeling: false,
      rational: true,
      dich3: 'negativist	judicious	objectivist	process',
      dich2: 'farsighted	yielding	dynamic	aristocratic	tactical	emotivist',
      dich4: 'asking'
    },
    {
      id: '13',
      socionicsName: 'eii',
      traits: {
        E: false,
        N: true,
        T: false,
        P: false
      },
      dichotomies: {},
      introverted: true,
      sensing: false,
      feeling: true,
      rational: true,
      dich3: 'positivist	judicious	objectivist	process',
      dich2: 'farsighted	yielding	static	aristocratic	strategic	constructivist',
      dich4: 'declaring'
    },
    {
      id: '14',
      socionicsName: 'iee',
      traits: {
        E: true,
        N: true,
        T: false,
        P: true
      },
      dichotomies: {},
      introverted: false,
      sensing: false,
      feeling: true,
      rational: false,
      dich3: 'negativist	judicious	objectivist	result',
      dich2: 'carefree	obstinate	static	aristocratic	tactical	emotivist',
      dich4: 'declaring'
    },
    {
      id: '15',
      socionicsName: 'sli',
      traits: {
        E: false,
        N: false,
        T: true,
        P: false
      },
      dichotomies: {},
      introverted: true,
      sensing: true,
      feeling: false,
      rational: false,
      dich3: 'positivist	judicious	objectivist	result',
      dich2: 'carefree	obstinate	dynamic	aristocratic	strategic	constructivist',
      dich4: 'asking'
    }
  ];

  const dichotomies = [
    {
      id: 'E',
      traits: ['E'],
      valid: 'Extrovert',
      null: 'Introvert'
    },
    {
      id: 'N',
      traits: ['N'],
      valid: 'Intuitive',
      null: 'Sensory'
    },
    {
      id: 'T',
      traits: ['T'],
      valid: 'Logical',
      null: 'Ethical'
    },
    {
      id: 'P',
      traits: ['P'],
      valid: 'Irrational',
      null: 'Rational'
    },
    {
      id: 'EN',
      traits: ['E', 'N'],
      valid: 'Carefree',
      null: 'Farsighted'
    },
    {
      id: 'ET',
      traits: ['E', 'T'],
      valid: 'Yielding',
      null: 'Obstinate'
    },
    {
      id: 'EP',
      traits: ['E', 'P'],
      valid: 'Static',
      null: 'Dynamic'
    },
    {
      id: 'NT',
      traits: ['N', 'T'],
      valid: 'Democratic',
      null: 'Aristocratic'
    },
    {
      id: 'NP',
      traits: ['N', 'P'],
      valid: 'Tactical',
      null: 'Strategic'
    },
    {
      id: 'TP',
      traits: ['T', 'P'],
      valid: 'Constructive',
      null: 'Emotive'
    },
    {
      id: 'ENT',
      traits: ['E', 'N', 'T'],
      valid: 'Positivist',
      null: 'Negativist'
    },
    {
      id: 'ENP',
      traits: ['E', 'N', 'P'],
      valid: 'Judicious',
      null: 'Decisive'
    },
    {
      id: 'ETP',
      traits: ['E', 'T', 'P'],
      valid: 'Merry',
      null: 'Serious'
    },
    {
      id: 'NTP',
      traits: ['N', 'T', 'P'],
      valid: 'Process',
      null: 'Results'
    },
    {
      id: 'ENTP',
      traits: ['E', 'N', 'T', 'P'],
      valid: 'Asking',
      null: 'Declaring'
    }
  ]

    return {types, dichotomies};
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