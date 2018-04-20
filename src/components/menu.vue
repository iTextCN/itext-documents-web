<style>
    .wrapper-header-nav .ivu-menu-item i{
        margin-right: 6px;
    }
    .wrapper-header .ivu-menu{
        z-index: 901;
    }
</style>
<template>
    <Menu mode="horizontal" :active-name="currentActiveKey" @on-select="handleSelect">
        <div class="wrapper-header-nav">
            <router-link to="/" class="wrapper-header-nav-logo">
                <img src="../../static/images/itext_nav.png">
            </router-link>
            <div class="wrapper-header-nav-list">
                <Menu-item name="guide">
                    <Icon type="ios-navigate"></Icon>
                    指南
                </Menu-item>
                <Menu-item name="component">
                    <Icon type="ios-keypad"></Icon>
                    index.component
                </Menu-item>
                <Menu-item name="live">
                    <Badge :dot="liveDot">
                        <Icon type="ios-videocam"></Icon>
                        index.live
                    </Badge>
                </Menu-item>
                <Menu-item name="practice">
                    <Icon type="ios-analytics"></Icon>
                    index.practice
                </Menu-item>
                <Submenu name="ecosystem">
                    <template slot="title">
                        <Icon type="ios-infinite"></Icon>
                        index.ecosystem
                    </template>
                    <Menu-item name="cli">
                        <!--<Icon type="settings"></Icon>-->
                        index.cli
                    </Menu-item>
                    <Menu-item name="iview-loader">
                        <!--<Icon type="settings"></Icon>-->
                        iView Loader
                    </Menu-item>
                    <Menu-item name="iview-admin">
                        iView Admin
                    </Menu-item>
                </Submenu>
                <!--<Select size="small" value="2" style="width: 60px;margin: 0 10px;" @on-change="handleVersion">-->
                    <!--<Option value="2">2.x</Option>-->
                    <!--<Option value="1">1.x</Option>-->
                <!--</Select>-->
                <ButtonGroup>
                    <Button type="ghost" size="small" icon="social-github" @click="handleGoToGitHub"></Button>
                    <Button type="ghost" size="small" icon="social-twitter" @click="handleGoToTwitter"></Button>
                </ButtonGroup>
            </div>
        </div>
    </Menu>
</template>
<script>
    import navigate from '../data/navigate';
//    import Config from '../config/config';
//    import bus from './bus';

    export default {
        props: {
            activeKey: String
        },
        data () {
            return {
                index: {},
                guide: {},
                navigateList: [],
                liveDot: false,
                currentActiveKey: this.activeKey
            };
        },
        watch: {
            activeKey (val) {
                this.currentActiveKey = val;
            },
            currentActiveKey (val) {
                this.$emit('on-change', val);
            }
        },
        methods: {
            handleSearch (path) {
                this.search = '';
                this.$refs.select.setQuery('');
                this.$nextTick(() => {
                    setTimeout(() => {
                        this.$router.push(path);
                    }, 300);
                });
            },
            handleSelect (type) {
                if (type === 'donate') {
                    bus.$emit('on-donate-show');
                } else if (type === 'github') {
                    window.open('https://github.com/iview/iview');
                } else if (type === 'guide') {
                    this.$router.push(navigate.guide[0].path);
                } else if (type === 'component') {
                    this.$router.push(navigate.beforeComponents[0].path);
                } else if (type === 'practice') {
                    this.$router.push(navigate.practice[0].path);
                } else if (type === 'cli') {
                    this.$router.push('/cli' + pathSuffix);
                } else if (type === 'live') {
                    this.$router.push('/live');
                } else if (type === 'iview-loader') {
                    this.$router.push('/docs/guide/iview-loader');
                } else if (type === 'iview-admin') {
                    window.open('https://github.com/iview/iview-admin');
                }
                this.$nextTick(() => {
                    this.updateActiveNav();
                });
            },
            updateActiveNav () {
                const componentList = [
                    '/docs/guide/install',
                    '/docs/guide/start',
                    '/docs/guide/i18n',
                    '/docs/guide/theme',
                    '/docs/guide/iview-loader',
                    '/overview',
                    '/docs/guide/update'
                ];

                const route = this.$route.path;
                if (route.indexOf('component') > -1 || componentList.indexOf(route) > -1) {
                    this.currentActiveKey = 'component';
                } else if (route.indexOf('practice') > -1) {
                    this.currentActiveKey = 'practice';
                } else if (route.indexOf('live') > -1) {
                    this.currentActiveKey = 'live';
                } else {
                    this.currentActiveKey = 'guide';
                }
            },
            handleVersion (v) {
                if (v == 1) {
                    window.location.href = 'http://v1.iviewui.com';
                }
            },
            handleGoToGitHub () {
                _hmt.push(['_trackEvent', 'menu-go-github', 'click']);
                window.open('https://github.com/iview/iview');
            },
            handleGoToTwitter () {
                _hmt.push(['_trackEvent', 'menu-go-twitter', 'click']);
                window.open('https://twitter.com/iViewUI');
            }
        },
        created () {
            let list = [];
            for (let i = 0; i < navigate.components.length; i++) {
                for (let j = 0; j < navigate.components[i].list.length; j++) {
                    list.push(navigate.components[i].list[j]);
                }
            }
            this.navigateList = list;
            // 设置直播 dot
            const liveDotVersion = window.localStorage.getItem('liveVersion');
            if (liveDotVersion) {
                this.liveDot = liveDotVersion < Config.liveVersion;
            } else {
                this.liveDot = true;
            }
        }
    };
</script>
