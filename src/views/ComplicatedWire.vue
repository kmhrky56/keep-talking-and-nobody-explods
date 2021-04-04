<template>
    <v-container fluid>
        <v-row>
            ワイヤーを{{cut()}}
        </v-row>
        <v-row>
            <v-col><v-btn @click="clearCheckboxWire">クリア</v-btn></v-col>
            <v-col><v-checkbox v-model="selectedWire" value="red"  label="赤"></v-checkbox></v-col>
            <v-col><v-checkbox v-model="selectedWire" value="blue" label="青"></v-checkbox></v-col>
            <v-col><v-checkbox v-model="selectedWire" value="star" label="星付き"></v-checkbox></v-col>
            <v-col><v-checkbox v-model="selectedWire" value="led"  label="LED点灯"></v-checkbox></v-col>
        </v-row>
        <v-row>
            <v-col><v-btn @click="clearCheckboxCase">クリア</v-btn></v-col>
            <v-col><v-checkbox v-model="selectedCase" value="odd"      label="シリアルナンバーの最後の数字が偶数か"></v-checkbox></v-col>
            <v-col><v-checkbox v-model="selectedCase" value="parallel" label="パラレルポート"></v-checkbox></v-col>
            <v-col><v-checkbox v-model="selectedCase" value="battery"  label="バッテリーが二本以上"></v-checkbox></v-col>
        </v-row>
    </v-container>
</template>
<script>
export default {
    name:"ComplicatedWire",
    data(){
        return {
            selectedCase:[],
            selectedWire:[],
        };
    },

    computed:{

    },

    methods:{
        clearCheckboxCase(){
            this.selectedCase = [];
        },

        clearCheckboxWire(){
            this.selectedWire = [];
        },

        cut(){
            const existsWire = t => this.selectedWire.some(e => {
                console.log(t); 
                return e == t.some(type => e == type);
            });
            const existsCase = c => this.selectedCase.some(e => e == c);

            // console.log(this.selectedWire);
            const CUT = "切る";
            const DONT_CUT = "切らない";

            let result = DONT_CUT;

            // 白のみ
            if(this.selectedWire.length == 0)
            {
                result = CUT;
            }

            // 星のみ
            if(this.selectedWire.length == 1 && existsWire(["star"]))
            {
                result = CUT;
            }

            // 星、LED バッテリー2本以上
            if(this.selectedWire.length == 2 && existsWire(["star", "led"] && existsCase("battery")))
            {
                result = CUT;
            }

            // 赤
            if(existsWire(["red"]))
            {
                // 赤のみ シリアルナンバー末尾が偶数
                if(this.selectedWire.length == 1 && existsCase("odd"))
                {
                    result = CUT;
                }

                // 赤、星
                if(this.selectedWire.length == 2 && existsWire(["star"]))
                {
                    result = CUT;
                }

                // (赤、LED) or (赤、星、LED) バッテリー2本以上
                if(!existsWire(["blue"]) && existsCase("battery"))
                {
                    result = CUT;
                }
            }

            // 青
            if(existsWire(["blue"]))
            {
                // 青のみ シリアルナンバー末尾が偶数
                if(this.selectedWire.length == 1 && existsCase("odd"))
                {
                    result = CUT;
                }

                // (青、LED) or (青、星、LED) パラレルポートあり
                if(!existsWire(["red"]) && existsCase("parallel"))
                {
                    result = CUT;
                }
            }

            // 赤、青
            if(existsWire(["red", "blue"]))
            {
                // (赤、青) or (赤、青、LED) シリアルナンバー末尾が偶数
                if(!existsWire(["star"]) && existsCase("odd"))
                {
                    result = CUT;
                }

                // 赤、青、星 パラレルポートあり
                if(this.selectedWire.length == 3 && existsWire(["star"]) && existsCase("parallel"))
                {
                    result = CUT;
                }
            }

            return result;
        }
    },
}    
</script>