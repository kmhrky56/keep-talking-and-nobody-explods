<template>
  <v-app>
    <v-tabs v-model="tab">
      <v-tabs-slider color="yellow"></v-tabs-slider>
      <v-tab v-for="item in tab_item" :key="item">
        {{item}}
      </v-tab>
    </v-tabs>
    <v-tabs-items v-model="tab">
      <v-tab-item>
        <SequenceWire></SequenceWire>
      </v-tab-item>
      <v-tab-item>
        <ComplicatedWire></ComplicatedWire>
      </v-tab-item>
      <v-tab-item>
      </v-tab-item>
    </v-tabs-items>
  </v-app>
</template>

<script>
import SequenceWire from '@/views/SequenceWire.vue';
import ComplicatedWire from '@/views/ComplicatedWire.vue';

export default {
  name: "App",

  components: {
    SequenceWire,
    ComplicatedWire
  },

  data: () => ({
    tab:null,
    tab_item:[
      "順番ワイヤ","複雑ワイヤ"
    ],
  }),

  methods:{
  }
};
</script>

<style>
.v-tabs{
  flex:unset !important;
}
</style>
