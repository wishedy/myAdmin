<template>
    <section class="main-container" :class="{'active':!toggleOnOff}">
        <el-header class="adminHeader">
            <el-menu
                class="el-menu-demo"
                mode="horizontal"
                background-color="#fff"
                text-color="#97a8be"
                active-text-color="#ffd04b">
                <Hamburger class="adminNav" @click.native.stop="toggleSide" :class="{'rotateClassName':toggleOnOff}"></Hamburger>
                <p class="adminTitle">后台管理系统</p>
                <div class="right-menu">
                    <section class="adminUser">
                        <section class="adminUserLogo">
                            <img src="https://p2.ssl.qhimgs1.com/bdr/326__/t01833006cd35e8478e.jpg" alt="">
                        </section>
                    </section>
                </div>
            </el-menu>
            <Tab class="adminTab" v-show="marTop"></Tab>
        </el-header>
        <router-view class="adminContent" :class="{'marTop':marTop}"></router-view>

    </section>
</template>
    <style lang="scss" scoped>
    .adminTab{
        background: #fff;
        height: 34px;
        border-bottom: 1px solid #d8dce5;
        -webkit-box-shadow: 0 1px 3px 0 rgba(0, 0, 0, 0.12), 0 0 3px 0 rgba(0, 0, 0, 0.04);
        box-shadow: 0 1px 3px 0 rgba(0, 0, 0, 0.12), 0 0 3px 0 rgba(0, 0, 0, 0.04);
    }
    .adminContent{
        width: 100%;
        min-height: 400px;
        margin-top:60px ;
        &.marTop{
            margin-top:88px;
        }
    }
    .main-container{
        min-height: 100%;
        margin-left: 36px;
        display: block;
        box-sizing: inherit;
        transition: margin-left .28s ease;
        width: 100%;
        /*position: fixed;
        top:0;*/
        .rotateClassName{
            transform: rotate(90deg);
            transition: all .28s ease;
        }
        &.active{
            margin-left: 180px;
            transition: margin-left .28s ease;
        }
        .adminHeader{
            z-index: 2;
            padding: 0 30px 0 0 !important;
            color:#97a8be;
            height: auto !important;
            position: fixed;
            top:0;
            width: 100%;

            /*.el-menu--horizontal{*/
                /*display: flex;*/
                /*flex-direction: row;*/
                /*justify-content: flex-start;*/
                /*width: 100%;*/
            /*}*/
            .adminNav{
                height: 50px;
                line-height: 58px;
                float: left;
                padding: 0 10px;
                &:focus{
                    outline: none;
                }
            }
            .adminTitle{
                line-height: 50px;
                font-family: "Helvetica Neue",Helvetica,"PingFang SC","Hiragino Sans GB","Microsoft YaHei","微软雅黑",Arial,sans-serif;
                font-size: 20px;
                float: left;
            }
            .right-menu {
                float: right;
                height: 100%;
                line-height: 50px;
                padding: 0 20px;
                margin: 0 150px 0 0;
                &:focus{
                    outline: none;
                }
                .right-menu-item {
                    display: inline-block;
                    margin: 0 8px;
                }
                .screenfull {
                    height: 20px;
                }
                .international{
                    vertical-align: top;
                }
                .theme-switch {
                    vertical-align: 15px;
                }
                .avatar-container {
                    height: 50px;
                    margin-right: 30px;
                    .avatar-wrapper {
                        cursor: pointer;
                        margin-top: 5px;
                        position: relative;
                        .user-avatar {
                            width: 40px;
                            height: 40px;
                            border-radius: 10px;
                        }
                        .el-icon-caret-bottom {
                            position: absolute;
                            right: -20px;
                            top: 25px;
                            font-size: 12px;
                        }
                    }
                }
                .adminUser{

                    img{
                        width: 40px;
                        height: 40px;
                        border-radius: 10px;
                    }


                }
            }

        }
    }
</style>
<script>
    import Tab from './tab/index'
    import Hamburger from './Hamburger/index';
    import {mapGetters,mapActions} from 'vuex'
    export default {
        data(){
            return {
               list:{}
            }
        },
        computed:{
            ...mapGetters(['toggleOnOff','nowTabData']),
            marTop(){
                return (this.nowTabData.length>2);
            }
        },
        methods:{
            ...mapActions(['toggleSide'])
        },
        components:{
            Hamburger,Tab
        }
    }
</script>
