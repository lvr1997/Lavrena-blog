<template>
    <MNavLinks title="前端生态" :items="frontendEnvironment">
        <Badge type="warning">常用网站</Badge>
    </MNavLinks>
    <MNavLinks title="AI" :items="ai">
        <Badge type="info">AI大模型</Badge>
    </MNavLinks>
    <MNavLinks title="工具相关" :items="tools">
        <Badge type="warning">实用工具</Badge>
    </MNavLinks>
    <MNavLinks title="大数据" :items="bigData">
        <Badge type="info">柱状图、条形图、各种图</Badge>
    </MNavLinks>
    <MNavLinks title="3D可视化" :items="web3D" >
        <Badge type="danger">三维世界</Badge>
    </MNavLinks>
    <MNavLinks title="低代码" :items="lowerCode">
        <Badge type="danger">效率神器</Badge>
    </MNavLinks>
    <MNavLinks title="大神文章" :items="HERO_ARTICLE">
        <Badge type="info">文章推荐</Badge>
    </MNavLinks>
</template>

<script setup lang="ts">
import MNavLinks from './MNavLinks.vue';
import { NAV_DATA } from './data';

const { frontendEnvironment,ai, tools, bigData, web3D,lowerCode, HERO_ARTICLE } = NAV_DATA
</script>