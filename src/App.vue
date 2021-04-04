<template>
  <v-app>
    <div class="wrap">
      <div class="sequence_wire">
        <v-container>
          <v-row justify="center">赤いワイヤの出現回数</v-row>
          <v-row>
            <v-col>ワイヤの出現回数</v-col>
            <v-col>切るべき接続先</v-col>
          </v-row>
          <v-row v-for="(color, index) in sequenceWire.red" :key="index" :class="{activeColor:color.isColor}" @click="color.isColor = !color.isColor">
            <v-col>{{index + 1}}番目の出現（赤）</v-col>
            <v-col>{{color.text}}</v-col>
          </v-row>
        </v-container>
        <v-container>
          <v-row justify="center">青いワイヤの出現回数</v-row>
          <v-row>
            <v-col>ワイヤの出現回数</v-col>
            <v-col>切るべき接続先</v-col>
          </v-row>
          <v-row v-for="(color, index) in sequenceWire.blue" :key="index" :class="{activeColor:color.isColor}" @click="color.isColor = !color.isColor">
            <v-col>{{index + 1}}番目の出現（青）</v-col>
            <v-col>{{color.text}}</v-col>
          </v-row>
        </v-container>
        <v-container>
          <v-row justify="center">黒いワイヤの出現回数</v-row>
          <v-row>
            <v-col>ワイヤの出現回数</v-col>
            <v-col>切るべき接続先</v-col>
          </v-row>
          <v-row v-for="(color, index) in sequenceWire.black" :key="index" :class="{activeColor:color.isColor}" @click="color.isColor = !color.isColor">
            <v-col>{{index + 1}}番目の出現（黒）</v-col>
            <v-col>{{color.text}}</v-col>
          </v-row>
        </v-container>
      </div>
    </div>
  </v-app>
</template>

<script>

export default {
  name: "App",

  components: {
  },

  data: () => ({
    sequenceWire:{
      red:[   {isColor:false,text:"C"},{isColor:false, text:"B"},{isColor:false,text:"A"},
              {isColor:false,text:"AかC"},{isColor:false, text:"B"},{isColor:false,text:"AかC"},
              {isColor:false,text:"AかBかC"},{isColor:false,text:"AかB"},{isColor:false, text:"B"}],
      blue:[  {isColor:false, text:"B"},{isColor:false,text:"AかC"},{isColor:false, text:"B"},
              {isColor:false,text:"A"},{isColor:false, text:"B"},{isColor:false, text:"BかC"},
              {isColor:false,text:"C"},{isColor:false,text:"AかC"},{isColor:false,text:"A"}],
      black:[ {isColor:false,text:"AかBかC"},{isColor:false,text:"AかC"},{isColor:false, text:"B"},
              {isColor:false,text:"AかC"},{isColor:false, text:"B"},{isColor:false, text:"BかC"},
              {isColor:false,text:"AかB"},{isColor:false,text:"C"},{isColor:false,text:"C"}]
    }
  }),
};
</script>

<style scoped>
 .sequence_wire{
   display: flex;
 }

 .activeColor{
   color: white;
   background-color: #444444;
 }
</style>
