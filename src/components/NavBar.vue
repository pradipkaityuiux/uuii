<template>
  <div class="navBar">
    <h2 class="title">PickUp <span>Line</span></h2>
    <Icon class="icon" icon="ic:round-play-arrow"/>
  </div>

</template>

<script>
import { Icon } from '@iconify/vue';
export default {
    name:"NavBar",
    components:{Icon}
}
</script>

<style scoped>
    .navBar{
        display: flex;
        align-items: center;
        justify-content: center;
        background-color: #3a00c0;
    }
    .title{
        font-size: 32px;
        margin-block: 16px;
        color: #fff;
    }
    .title span{
        color: #fc2069;
        background-color: #fff;
        padding: 5px 10px;
        border-radius: 10px;
    }
    .icon{
        color: #fff;
        width: 32px;
        height: 32px;
    }
</style>