<template>
  <v-app>
    <h1> LEFT + 100%</h1>
    <AppListOverflowed class="margin" align="left" :items="whatsNext" />
    <h1> CENTER + 100%</h1>
    <AppListOverflowed class="margin" align="center" :items="whatsNext" />
    <h1> LEFT + 50% & CENTER + 50%</h1>
    <div class="margin d-flex"  >
      <AppListOverflowed class="w-50"  align="left" :items="whatsNext" />
      <AppListOverflowed class="w-50" align="center"  :items="whatsNext" />
    </div>
  </v-app>
</template>

<script>
import AppListOverflowed from './components/AppListOverflowed';

export default {
  name: 'App',
  components: {
    AppListOverflowed,
  },
  data: () => ({
    whatsNext: [

      {
        text: 'Explore components',
      },
      {
        text: '12312312',
      },
      {
        text: '2342342',
      },
      {
        text: 'Explore components',
      },
      {
        text: 'Explore components',
      },
      {
        text: 'Explore components',
      },
      {
        text: 'Explore components',
      },
      {
        text: 'Explore components',
      },
    ],
  }),
};
</script>
<style>
.hello{
  width: 300px;
}
.margin{
  margin:  10px 0;
}
.w-50{
  width: 50%;
}
</style>
