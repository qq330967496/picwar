
<template>
    <header>
        <div class="header_main">
            <div class="logo">
                {{text}}
            </div>
            <router-link class="list-group-item" :to="{ path: '/home'}">静态.png</router-link>
            <router-link class="list-group-item" :to="{ path: '/test'}">动态.gif</router-link>
            <!--<router-link class="list-group-item" :to="{ path: '/about'}">About</router-link>-->
            <!--<router-link class="list-group-item" :to="{ path: '/test'}">Test</router-link>-->
        </div>
    </header>
</template>

<script>
    export default{
        data(){
            return{
                text:'PicWar'
            }
        }
    }
</script>
