<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Tab 3</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Tab 3</ion-title>
        </ion-toolbar>
      </ion-header>

      <svg id="gantt"></svg>
      
      <ExploreContainer name="Tab 3 page" />
    </ion-content>
  </ion-page>
</template>

<script>
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent } from '@ionic/vue';
import ExploreContainer from '@/components/ExploreContainer.vue';

export default  {
  name: 'Tab3',
  components: { ExploreContainer, IonHeader, IonToolbar, IonTitle, IonContent, IonPage },
  mounted: function() {
    const tasks = [
  {
    id: 'Task 1',
    name: 'Redesign website 1',
    start: '2016-12-28',
    end: '2016-12-31',
    progress: 20,
    dependencies: 'Task 2',
    custom_class: 'bar-milestone-1' // optional
  },
  {
    id: 'Task 2',
    name: 'Redesign website 2',
    start: '2016-12-25',
    end: '2017-01-02',
    progress: 20,
    dependencies: '',
    custom_class: 'bar-milestone-1' // optional
  },
  {
    id: 'Task 3',
    name: 'Redesign website 3',
    start: '2016-01-28',
    end: '2016-02-20',
    progress: 20,
    dependencies: 'Task 1',
    custom_class: 'bar-milestone-1' // optional
  },
  {
    id: 'Task 4',
    name: 'Redesign website 4',
    start: '2016-12-28',
    end: '2016-12-31',
    progress: 20,
    dependencies: 'Task 2, Task 3',
    custom_class: 'bar-milestone', // optional
    periods: [
	{
		start: '2017-01-05',
	end: '2017-01-07'
 },
	{
		start: '2017-01-09',
		end: '2017-01-14'
},
	{
		start: '2017-01-15',
		end: '2017-01-17'
  }
   ]
  }
];
const gantt = new Gantt("#gantt", tasks, {
    header_height: 50,
    column_width: 30,
    step: 24,
    view_modes: ['Quarter Day', 'Half Day', 'Day', 'Week', 'Month'],
    bar_height: 20,
    bar_corner_radius: 3,
    arrow_curve: 5,
    padding: 18,
    view_mode: 'Day',   
    date_format: 'YYYY-MM-DD',
    custom_popup_html: null
});
  }
}
</script>

