<style lang="less">
    @import "../../static/styles/article.less";
</style>
<template>
    <div>
        <div class="wrapper">
            <div class="wrapper-header">
                <nav-menu :active-key="activeKey" @on-change="handleNavMenuChange"></nav-menu>
            </div>
            <div class="wrapper-container">
                <Row>
                    <i-col span="4" class="wrapper-navigate">
                        <Navigate :type="activeKey"></Navigate>
                    </i-col>
                    <i-col span="20">
                        <div class="wrapper-content ivu-article">
                            <slot></slot>
                        </div>
                    </i-col>
                </Row>
            </div>
        </div>
        <div class="footer">
            <div class="footer-main">
                <Row>
                    <i-col span="5">
                        <h4>
                            <Icon type="social-github"></Icon>
                            GitHub
                        </h4>
                        <ul>
                            <li>
                                <a href="https://github.com/iview/iview" target="_blank">iView</a>
                            </li>
                            <li>
                                <a href="https://github.com/iview/iview-cli" target="_blank">iView Cli</a>
                            </li>
                            <li>
                                <a href="https://github.com/iview/iview-admin" target="_blank">iView Admin</a>
                            </li>
                            <li>
                                <a href="https://github.com/iview/iview-doc" target="_blank">iView Doc</a>
                            </li>
                            <li>
                                <a href="https://github.com/iview/iview-project" target="_blank">iView Project</a>
                            </li>
                        </ul>
                    </i-col>
                    <i-col span="5">
                        <h4>
                            <Icon type="link"></Icon>
                            {{ index.links }}
                        </h4>
                        <ul>
                            <li>
                                <a href="https://www.talkingdata.com/" target="_blank">TalkingData</a> - {{ index.td }}
                            </li>
                            <li>
                                <a href="http://mi.talkingdata.com/" target="_blank">Marketing Intelligence</a> - {{ index.td_mi }}
                            </li>
                            <li>
                                <a href="https://github.com/TalkingData/Fregata" target="_blank">Fregata</a> - {{ index.Fregata }}
                            </li>
                            <li>
                                <a href="https://github.com/TalkingData/Myna" target="_blank">Myna</a> - {{ index.Myna }}
                            </li>
                            <li>
                                <a href="https://github.com/TalkingData/owl" target="_blank">OWL</a> - {{ index.OWL }}
                            </li>
                        </ul>
                    </i-col>
                    <i-col span="5" offset="2">
                        <h4>
                            <Icon type="chatbubbles"></Icon>
                            {{ index.community }}
                        </h4>
                        <ul>
                            <li>
                                <a href="https://github.com/iview/iview/issues" target="_blank">{{ index.feedback }}</a>
                            </li>
                            <li>
                                <a href="https://www.iviewui.com/new-issue" target="_blank">{{ index.bug }}</a>
                            </li>
                            <li>
                                <a href="https://gitter.im/iview/iview" target="_blank">{{ index.chat }}</a>
                            </li>
                            <li>
                                <a href="https://segmentfault.com/t/iview" target="_blank">SegmentFault</a>
                            </li>
                        </ul>
                    </i-col>
                    <i-col span="5" offset="2">
                        <div class="footer-aside">
                            <div class="footer-logo">
                                <img src="../../static/images/itext_nav.png">
                            </div>
                        </div>
                    </i-col>
                </Row>
            </div>
        </div>
        <div class="catalogue" v-show="list.length">
            <card dis-hover shadow>
                <div class="catalogue-title">
                    <template v-if="lang === 'zh-CN'">目录</template>
                    <template v-else>CAT</template>
                </div>
                <div class="catalogue-content">
                    <ul>
                        <li v-for="item in list">
                            <a :href="'#' + item">{{ item }}</a>
                        </li>
                        <li>
                            <a href="#API">API</a>
                        </li>
                    </ul>
                </div>
            </card>
        </div>
        <!--<Modal v-model="donate" v-if="lang === 'zh-CN'" title="支持 iView 的开发" @on-ok="handleModalClose" @on-cancel="handleModalClose" class-name="vertical-center-modal">-->
            <!--<div class="ivu-article">-->
                <!--<p>iView 是采用 MIT 许可的开源项目，您可以在个人或企业项目中免费使用。不过，如果您觉得 iView 对您的项目带来了帮助，提高开发效率，可以用捐助来表示您的谢意：)</p>-->
                <!--<p>您可以用公司的名义进行赞助，赞助信息将在文档页展示。联系邮箱 <a href="mailto:admin@aresn.com">admin@aresn.com</a></p>-->
                <!--<h3>个人可使用 微信 或 支付宝 捐助：</h3>-->
                <!--<div>-->
                    <!--<img src="../../static/images/pay.png" style="width: 100%">-->
                <!--</div>-->
            <!--</div>-->
        <!--</Modal>-->
        <!--<Modal v-model="donate" title="与 iView 合作，有效触达技术人群" @on-ok="handleModalClose" @on-cancel="handleModalClose" width="600" class-name="vertical-center-modal">-->
            <!--<div class="ivu-article">-->
                <!--<p>如果您有品牌推广、活动推广、招聘推广、社区合作的需求，欢迎联系我们。</p>-->
                <!--<p>联系邮箱 <a href="mailto:admin@aresn.com">admin@aresn.com</a> 咨询。</p>-->
                <!--<p>广告位如下图所示：</p>-->
                <!--<div>-->
                    <!--<Carousel v-if="donate" v-model="adCarousel" loop autoplay :autoplay-speed="3000" dots="outside">-->
                        <!--<CarouselItem>-->
                            <!--<div class="demo-carousel" style="height: 300px">-->
                                <!--<img src="../../static/images/ad-demo1.png" style="width: 100%">-->
                            <!--</div>-->
                        <!--</CarouselItem>-->
                        <!--<CarouselItem>-->
                            <!--<div class="demo-carousel" style="height: 300px;">-->
                                <!--<img src="../../static/images/ad-demo2.png" style="width: 100%">-->
                            <!--</div>-->
                        <!--</CarouselItem>-->
                    <!--</Carousel>-->
                <!--</div>-->
            <!--</div>-->
        <!--</Modal>-->
        <!--<Modal v-model="donate" v-if="lang !== 'zh-CN'" title="Donate iView project" @on-ok="handleModalClose" @on-cancel="handleModalClose" class-name="vertical-center-modal">-->
            <!--<div class="ivu-article">-->
                <!--<p>iView is an open source project with MIT licenses that you can use for free in your personal or business projects. However, if you feel that iView has helped your project to improve development efficiency, you can use donations to express your gratitude: )</p>-->
                <!--<h3>Use Wechat or Alipay to donate：</h3>-->
                <!--<div>-->
                    <!--<img src="../../static/images/pay.png" style="width: 100%">-->
                <!--</div>-->
            <!--</div>-->
        <!--</Modal>-->
        <!--<Modal v-model="ask" title="免费加入 iView 官方QQ群参与讨论" class-name="vertical-center-modal">-->
            <!--<div class="ivu-article">-->
                <!--<p>免费加入官方QQ讨论群，交流 iView 技术问题。</p>-->
                <!--<p>群号：<strong>623520058</strong></p>-->
                <!--<p>二维码：</p>-->
                <!--<p>-->
                    <!--<img src="../../static/images/qqgroup2.png" style="display: block;width: 50%;margin: 0 auto;">-->
                <!--</p>-->
                <!--<p>-->
                    <!--<Alert show-icon>仅限开发者加入，请勿讨论与技术无关的问题，比如发招聘信息等。</Alert>-->
                <!--</p>-->
            <!--</div>-->
        <!--</Modal>-->
        <!--&lt;!&ndash; todo 提问 &ndash;&gt;-->
        <!--<div class="ask-question" @click="ask = true" v-if="lang === 'zh-CN'">-->
            <!--<Icon type="ios-people" size="24"></Icon>-->
            <!--<p>QQ群</p>-->
        <!--</div>-->
    </div>
</template>
<script>
    import Navigate from '../components/navigate.vue';
    import navigate from '../data/navigate';
    import navMenu from './menu.vue';
//    import bus from './bus';

    export default {
        components: {
            Navigate,
            navMenu
        },
        data () {
            return {
                list: [],
                donate: false,
                ask: false,
                activeKey: '',
                lang: this.$lang,
                adCarousel: 0,
                index: {},
                link: {}
            }
        },
        methods: {
            handleModalClose () {
                this.donate = false;
            },
            handleAskClose () {
                this.ask = false;
            },
            updateActiveNav () {
                const componentList = [
                    '/docs/guide/install',
                    '/docs/guide/install-en',
                    '/docs/guide/start',
                    '/docs/guide/start-en',
                    '/docs/guide/i18n',
                    '/docs/guide/i18n-en',
                    '/docs/guide/theme',
                    '/docs/guide/theme-en',
                    '/docs/guide/iview-loader',
                    '/docs/guide/iview-loader-en',
                    '/overview',
                    '/overview-en',
                    '/docs/guide/update',
                    '/docs/guide/update-en'
                ];

                const route = this.$route.path;
                if (route.indexOf('component') > -1 || componentList.indexOf(route) > -1) {
                    this.activeKey = 'component';
                } else if (route.indexOf('practice') > -1) {
                    this.activeKey = 'practice';
                } else if (route.indexOf('live') > -1) {
                    this.activeKey = 'live';
                }  else {
                    this.activeKey = 'guide';
                }
            },
            handleNavMenuChange (val) {
                this.activeKey = val;
            }
        },
        created () {
            this.lang = this.$lang;
        },
        mounted () {
            this.updateActiveNav();

            const examples = this.$slots.default[0].elm.querySelectorAll('.example');

            for (let i = 0; i < examples.length; i++) {
                const title = examples[i].querySelectorAll('header span a')[0].getAttribute('href').replace('#', '');
                this.list.push(title);
            }
        }
    }
</script>
