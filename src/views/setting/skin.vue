<!------------ choice theme ------------>
<template>
    <div class="win fr" id="choice-theme">
        <!--Multi-handle fixed -->
        <multi-handle :routerLink="'/dashboard'"></multi-handle>
        <div class="wm">
            <!--tit-->
            <p class="win-tit"><span>▌</span>&nbsp;切换主题</p>
            <!--cover-->
            <el-carousel :interval="8000" type="card" height="300px">
                <el-carousel-item v-for="item in 6" :key="item">
                    <img :src='imgsrc + item + ".jpg"' alt="xxx" @click="selectSkin(item)">
                    <h3>{{ item }}</h3>
                </el-carousel-item>
            </el-carousel>
            <!--show-->
            <el-card class="box-card">
                <div class="box-item">
                    <div class="fl">
                        <span>当前皮肤：</span>
                        <span class="primary">{{skinname}}</span>
                    </div>
                    <div class="fr">
                        <span class="field-label">切换为默认皮肤：</span>
                        <el-switch v-model="theme" on-text="" off-text="" :disabled="normalsw"></el-switch>
                    </div>
                </div>
            </el-card>
            <!--display color-->
            <div class="block">
                <span class="wrapper">
                    <el-button type="success">成功按钮</el-button>
                    <el-button type="warning">警告按钮</el-button>
                    <el-button type="danger">危险按钮</el-button>
                    <el-button type="info">信息按钮</el-button>
                 </span>
            </div>
            <div class="block">
                <el-tag class='tag-item' v-for="tag in tags" :type="tag.type" :key='tag.type'>
                    {{tag.name}}
                </el-tag>
            </div>
        </div>
    </div>
</template>
<script>
    import {replaceClass} from '../../utils/index';
    export default {
        name:'choice-theme',
        data() {
            return {
                theme: true,
                imgsrc: 'http://otaflb4oo.bkt.clouddn.com/mimo/theme/cover/cover',
                skinname: '标准皮肤',
                normalsw:true,
                tags: [
                    {
                        name: '标签一',
                        type: ''
                    },
                    {
                        name: '标签二',
                        type: 'gray'
                    },
                    {
                        name: '标签三',
                        type: 'primary'
                    },
                    {
                        name: '标签四',
                        type: 'success'
                    },
                    {
                        name: '标签五',
                        type: 'warning'
                    },
                    {
                        name: '标签六',
                        type: 'danger'
                    }
                ],
                inputVisible: false,
                inputValue: ''
            }
        },
        watch: {
            theme() {
                replaceClass(document.body, 'custom-theme-normal');
                this.skinname = '标准皮肤';
                this.normalsw = true;
                //   this.$store.dispatch('setTheme', value);
            }
        },
        created(){
            this.sw();
        },
        methods: {
            sw(){
                const className = document.body.className;
                if (className === 'custom-theme-normal' || className === '') {
                    this.skinname = '标准皮肤';
                    this.theme = true;
                    this.normalsw = true;
                }
                else {
                    this.theme = false;
                    this.normalsw = false;
                }
            },
            choiceTem(status){
                const statusMap = {
                    1: 'custom-theme-normal',
                    2: 'custom-theme-blackhole',
                    3: 'custom-theme-spring',
                    4: 'custom-theme-goldenyear',
                    5: 'custom-theme-changeself',
                    6: 'custom-theme-pinktemptation',
                };
                return statusMap[status]
            },
            skinName(status){
                const statusMap = {
                    1: '标准皮肤',
                    2: '黑色奢华',
                    3: '绿意盎然',
                    4: '金色时代',
                    5: '放飞自我',
                    6: '粉色诱惑',
                };
                return statusMap[status]
            },
            selectSkin(n){
                replaceClass(document.body, this.choiceTem(n));
                this.skinname = this.skinName(n);
                this.sw();
            }
        }
    };
</script>
<style rel="stylesheet/scss" lang="scss" scoped>
    $card-height: 30px;
    #choice-theme{
        .box-card {
            width: 400px;
            margin: 20px auto;
            .box-item {
                height: $card-height;
                div {
                    height: 100%;
                    line-height: $card-height;
                    .primary {
                        font-size: 16px;
                    }
                }
            }
        }
        .el-carousel__item {
            img {
                width: 100%;
                height: 100%;
            }
        }
        .block {
            padding: 15px 25px;
        }
        .tag-item {
            margin-right: 15px;
        }
    }
</style>

