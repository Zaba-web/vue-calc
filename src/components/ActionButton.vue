<template>
    <div class="button-container" :style="{background: color, width:size}" @click="SendVal">
        {{ value }}
    </div>
</template>

<script>

export default {
    name:"ActionButton",
    props: ["value", "color", "size"],
    methods:{
        SendVal: function(){
            this.$emit("GetVal", this.value);
        }
    }
}
</script>>

<style scoped>
    .button-container{
        display:flex;
        height:40px;
        justify-content: center;
        align-items: center;
        border-radius: 100px;
        cursor: pointer;
        transition: .3s;
        color:#fff;
        font-family: 'Courier New', Courier, monospace;
        font-size:20px;
        margin:3px;
    }
    .button-container:hover{
        filter: brightness(1.5);
    }
</style>