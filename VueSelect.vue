<template>
<div class="options" @click="toggleOptions()" @mouseout="hideOptions()">
    <div class="label">{{nowName||placeholder}}</div>
    <ul class="option-list" :class="showClass" @mousemove="showOptions()">
        <li v-for="(item,index) in options" :key="index" @click="handleSelect(index)">{{item[name]}}</li>
    </ul>
</div>
</template>

<script>
export default {
    model: {
        event: 'select',
        prop: 'nowValue',
    },
    props: {
        label: String,
        options: Array,
        name:{
            type:String,
            default: 'name'
        },
        value:{
            default: 'value'
        },
        placeholder: String,
        nowValue:{
            default:""
        }
    },
    data() {
        return {
            showClass:"",
            nowName:""
        }
    },
    watch: {
        nowValue(newVal,oldVal){
            this.options.find((item,index)=>{
                if(item[this.value]==newVal){
                    this.nowName = item[this.name]
                }
            })
        }
    },
    methods: {
        showOptions(){
            this.showClass = "show"
        },
        hideOptions(){
            this.showClass = ""
        },
        toggleOptions:function(){
            if(this.showClass == "show"){
                this.hideOptions()
            }else{
                this.showOptions()
            }
        },
        handleSelect: function(index){
            setTimeout(()=>{
                this.hideOptions()
            },100)
            let nowValue = this.options[index][this.value]
            this.nowName = this.options[index][this.name]
            this.$emit('select', nowValue)
            this.$emit('change', this.options[index])
        }
    }
}
</script>

<style scoped>
/* select选择框 */
.options{
    position: relative;
    height: 35px;
    box-sizing: border-box;
    line-height: 35px;
    background-color: #fff;
    cursor: pointer;
}
.options .label{
    padding: 0 10px;
    position: relative;
    user-select: none;
}
.options .label:after{
    content: "";
    height: 0;
    width: 0;
    position: absolute;
    top: 6px;
    bottom: 0;
    right: 10px;
    margin: auto;
    border-width: 6px;
    border-style: solid;
    border-color:#cccccc transparent transparent transparent ;
}
.options .option-list{
    position: absolute;
    z-index: 9;
    top: 35px;
    height: 0;
    overflow: hidden;
    /* margin-top: 5px; */
    min-width: 100%;
    max-width: 180%;
    box-sizing: border-box;
    background-color: #fff;
    box-shadow: 0 0 15px #dedede;
    transition: .2s
}
.options .option-list.show{
    height: auto;
    max-height: 300px;
    overflow: auto;
    overflow-x: hidden;
}
.option-list li{
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    padding: 0 10px;
    border-bottom: 1px solid #f7f7f7;
    cursor: pointer;
}
.option-list li:hover{
    background-color: #f7f7f7
}
</style>
