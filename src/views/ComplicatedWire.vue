<template>
    <v-container fluid>
        <v-row>
            ワイヤーを{{cut}}
        </v-row>
        <v-row>
            <v-btn @click="clearCheckbox">クリア</v-btn>
        </v-row>
        <v-row>
            <v-col><v-checkbox v-model="selected" value="red"  label="赤"></v-checkbox></v-col>
            <v-col><v-checkbox v-model="selected" value="blue" label="青"></v-checkbox></v-col>
            <v-col><v-checkbox v-model="selected" value="star" label="星付き"></v-checkbox></v-col>
            <v-col><v-checkbox v-model="selected" value="led"  label="LED点灯"></v-checkbox></v-col>
        </v-row>
        <v-row>
            <v-col><v-checkbox v-model="selected" value="odd"      label="シリアルナンバーの最後の数字が偶数か"></v-checkbox></v-col>
            <v-col><v-checkbox v-model="selected" value="parallel" label="パラレルポート"></v-checkbox></v-col>
            <v-col><v-checkbox v-model="selected" value="battery"  label="バッテリーが二本以上"></v-checkbox></v-col>
        </v-row>
    </v-container>
</template>
<script>
export default {
    name:"ComplicatedWire",
    data(){
        return {
            selected:[],
        };
    },

    computed:{
        cut(){
            if( this.selected.length == 0 || ( this.selected.length == 1 && this.selected.find(e => e == "star") ) || 
                (this.selected.length == 3 && this.selected.every(e => e == "star" || e == "led" || e == "battery")) )
            {
                return "切る";
            }

            if(this.selected.find(e => e == "red") && this.selected.length >= 2)
            {
                if(this.selected.length == 2 && this.selected.some(e => e == "star" || e == "odd"))
                {
                    return "切る";
                }

                if(this.selected.some(e => e == "battery"))
                {
                    if(this.selected.length == 3 && this.selected.some(e => e == "led"))
                    {
                        return "切る";
                    }

                    if(this.selected.length == 4 && this.selected.some(e => e == "led") && this.some(e => e == "star"))
                    {
                        return "切る";
                    }
                }
            }

            if(this.selected.find(e => e=="blue"))
            {
                if(this.selected.length == 2 && this.selected.some(e => e == "odd"))
                {
                    return "切る";
                }

                if(this.selected.some(e => e == "parallel"))
                {
                    if( (this.selected.length == 3 && this.selected.some( e => e == "led") ) ||
                        (this.selected.length == 4 && this.selected.some( e => e == "led") && this.selected.some(e => e == "star") ) 
                    )
                    {
                        return "切る";
                    }
                }

            }

            if(this.selected.find(e => e == "blue") && this.selected.find(e => e == "red"))
            {
                if(this.selected.length == 3 && this.selected.some(e => e == "odd"))
                {
                    return "切る";
                }

                if(this.selected.length == 4 && this.selected.some(e => e == "star") && this.selected.some(e => e == "parallel"))
                {
                    return "切る";
                }

                if(this.selected.length == 4 && this.selected.some(e => e == "led") && this.selected.some(e => e == "odd") )
                {
                    return "切る";
                }
            }

            return "切らない";
        }
    },

    methods:{
        clearCheckbox(){
            this.selected = [];
        }
    },
}    
</script>