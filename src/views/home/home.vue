<template>
  <div class="home">
    <div :style="htmlHeight" class="header-wrap">
      <header class="full_page" id="page-header" ref="kk">
        <!-- <log_nav
          v-show="rocketheight<100?true:false"
          @myhide="home_hide_byvalue"
          :home_hide="home_hide"
          :windowWidth="windowWidth"
          v-on:listenchangepage="showchangepages"
        ></log_nav>
        <log_nav1
        v-if="this.scrollStep<0?true:false"
        v-show="rocketheight<100?false:true"
          @myhide="home_hide_byvalue"
          :home_hide="home_hide"
          :windowWidth="windowWidth"></log_nav1> -->
        <!-- 以上是导航 -->
        <div class="header-bottom">
          <div class="print">
            <h1>Pander</h1>
            <!-- 动态变化的内容-->
            <div class="print-bootom">
              <p class="typer-dynamic">
                <span class="cut">
                  <span
                    class="word"
                    v-for="(letter, index) in words"
                    :key="index"
                    >{{ letter }}</span
                  >
                </span>
                <!-- 模拟光标-->
                <span class="typer-cursor"></span>
              </p>
            </div>
          </div>
          <span @click="scroll_bottom" class="header-bottom-slop">
            <svg
              t="1624608588319"
              class="icon"
              viewBox="0 0 1603 1024"
              version="1.1"
              xmlns="http://www.w3.org/2000/svg"
              p-id="2380"
              width="20"
              height="20"
            >
              <path
                d="M1010.042131 836.203222L837.472119 1008.773234c-18.610492 18.610492-50.755886 18.610492-71.05824 0L15.226766 255.894259c-18.610492-18.610492-18.610492-50.755886 0-71.058241L187.796778 13.957869c18.610492-18.610492 50.755886-18.610492 71.058241 0l751.187112 751.187112c18.610492 20.302354 18.610492 52.447749 0 71.058241z"
                p-id="2381"
                fill="#ffffff"
              ></path>
              <path
                d="M1416.089219 13.957869L1588.659232 186.527881c18.610492 18.610492 18.610492 50.755886 0 71.05824L835.780256 1008.773234c-18.610492 18.610492-50.755886 18.610492-71.05824 0L593.843866 836.203222c-18.610492-18.610492-18.610492-50.755886 0-71.058241L1346.722842 13.957869c18.610492-18.610492 50.755886-18.610492 69.366377 0z"
                p-id="2382"
                fill="#ffffff"
              ></path>
            </svg>
          </span>
        </div>
      </header>
      <phone_home
        v-if="windowWidth < 1200"
        :log_title1="log_title"
        :log_content1="log_content"
        :log_date1="log_date"
        :log_img_srcs1="log_img_srcs"
      ></phone_home>
      <div v-if="windowWidth > 1200" class="content-container">
        <div class="content-left">
          <!-- log-item组件刷新 -->
             <component :is="currentvue"></component>

          <div v-if="currentvue==null" v-for="(index, item) in log_img_srcs.length">
            <log_item
              v-if="item % 2 == 0"
              :log_img_srcs="log_img_srcs[item]"
              :log_date="log_date[item]"
              :log_content="log_content[item]"
              :log_title="log_title[item]"
            ></log_item>
            <log_item2
              v-else-if="item % 2 != 0"
              :log_img_srcs="log_img_srcs[item]"
              :log_date="log_date[item]"
              :log_content="log_content[item]"
              :log_title="log_title[item]"
            ></log_item2>
          </div>
        </div>
        <div class="content-right">
          <log_card></log_card>
          <notice></notice>

          <new_article
            :new_article_date="log_date"
            :new_article_img_src="log_img_srcs"
            :new_article_title="log_title"
          ></new_article>
          <classify></classify>
          <logtag></logtag>
          <archive
            :aritem_item_count="archive_count"
            :aritem_item_date="archive_date"
          ></archive>
          <log_info
            :log_info_count="log_info_count"
            :log_info_title="log_info_title"
          ></log_info>
        </div>
       
      </div>
        <div style="clear: both"></div>
    <log_bottom v-if="windowWidth > 1200" ></log_bottom>
    </div>
   
    <!-- <transition name="slide-fade">
      <div v-show="rocketshow" @click="hh" id="rocket">
        <svg
          t="1624883837608"
          class="icon"
          viewBox="0 0 1024 1024"
          version="1.1"
          xmlns="http://www.w3.org/2000/svg"
          p-id="6433"
          width="50"
          height="50"
        >
          <path
            d="M404.0704 372.224V231.936s-0.0512-94.5152 133.8368-155.2896c40.3968 17.7664 94.464 68.864 105.0624 154.0608v108.4928l-32.8192 49.664s-57.3952-94.7712-100.608-116.8384c-25.088 22.6816-73.5744 94.2592-79.9744 121.7536-16.896 17.664-19.1488-15.0016-25.4976-21.5552z"
            fill="#E56A77"
            p-id="6434"
          ></path>
          <path
            d="M154.368 824.9856v20.0192c0 18.2272 14.7968 33.024 33.024 33.024h225.28v-273.7664l-245.76 194.816a33.21344 33.21344 0 0 0-12.544 25.9072z"
            fill="#BC9BE0"
            p-id="6435"
          ></path>
          <path
            d="M322.56 296.192S226.304 349.1328 226.304 452.6592v264.9088l192.512-162.2528V452.6592C418.7648 335.872 322.56 296.192 322.56 296.192zM736.6144 301.312s93.6448 52.9408 93.6448 156.4672v264.9088l-187.2384-162.2528V457.7792c-0.0512-116.7872 93.5936-156.4672 93.5936-156.4672z"
            fill="#FFA750"
            p-id="6436"
          ></path>
          <path
            d="M642.9696 591.2064v286.8736h238.336c18.944 0 34.3552-15.36 34.3552-34.3552v-20.736c0-10.496-4.8128-20.4288-13.056-26.9312l-259.6352-204.8512zM606.3616 503.9616c0-146.3808-75.8272-200.3456-75.8272-200.3456S446.2592 360.448 446.2592 503.9616v374.0672h160.1536c-0.0512 0.0512-0.0512-227.6864-0.0512-374.0672z"
            fill="#BC9BE0"
            p-id="6437"
          ></path>
          <path
            d="M348.1088 971.6224h-44.4416c-11.6224 0-21.7088-7.7312-24.2688-18.6368l-11.6224-49.3056h119.0912l-14.8992 50.5344c-2.9696 10.2912-12.7488 17.408-23.8592 17.408zM762.8288 971.6224h-44.4416c-11.6224 0-21.7088-7.7312-24.2688-18.6368l-11.6224-49.3056h119.0912l-14.8992 50.5344c-2.9696 10.2912-12.7488 17.408-23.8592 17.408z"
            fill="#FFA750"
            p-id="6438"
          ></path>
          <path
            d="M910.336 772.9664l-64.768-51.0976V443.1872c0-136.6528-120.5248-184.9856-121.7536-185.4464-4.096-1.5872-8.704-1.3312-12.5952 0.6656-1.8432 0.9728-19.6608 10.3936-41.0624 28.3648v-40.7552c0-150.016-152.064-202.5472-153.6-203.0592a15.1552 15.1552 0 0 0-11.1104 0.5632c-6.1952 2.7648-152.2176 69.376-152.2176 202.496V286.72c-24.832-20.1216-46.4384-28.7744-46.9504-28.9792-4.096-1.5872-8.704-1.3312-12.5952 0.6656-4.9152 2.56-120.2176 63.5904-120.2176 184.7296v282.3168l-59.904 47.5136a54.016 54.016 0 0 0-20.5824 42.5472v23.6032c0 29.952 24.3712 54.3232 54.3232 54.3232h69.4784l12.6976 55.9104c5.0176 22.1696 24.4224 37.632 47.1552 37.632h58.88c21.504 0 40.6528-14.4384 46.4896-35.1232l16.5888-58.4192h229.1712l16.5888 58.4192c5.888 20.6848 24.9856 35.1232 46.4896 35.1232h58.88c22.7328 0 42.1376-15.4624 47.1552-37.632l12.6976-55.9104h67.1744c29.952 0 54.3232-24.3712 54.3232-54.3232v-23.5008c-0.0512-16.7424-7.5776-32.3072-20.736-42.6496z m-270.848-455.7824c-13.3632 15.6672-25.856 34.5088-34.8672 56.576-8.5504-24.2176-19.4048-44.0832-30.5664-60.0064h65.4336v3.4304z m-17.7664 187.8016h193.1264v35.072h-193.1264v-35.072z m32.4096 65.792h160.768v126.8224l-0.5632-0.4608-160.2048-126.3616z m65.024-281.4464c22.3744 11.1104 95.744 55.1424 95.744 153.856v31.1296h-193.1264v-31.1296c0-44.9024 19.8144-80.5888 42.0864-106.5984 1.792-1.28 3.2768-2.9696 4.352-4.9152 19.8656-21.8624 40.8064-36.1472 50.944-42.3424z m-206.592-215.1424c25.7024 10.24 126.9248 57.9072 126.9248 171.776v37.0176h-91.392c-16.5376-16.1792-29.696-23.6544-31.232-24.4736a15.42144 15.42144 0 0 0-16.384 1.0752c-1.3312 0.9728-11.776 8.7552-25.6 23.3984H383.9488v-37.0176c0-99.7888 103.4752-158.8736 128.6144-171.776z m-308.3776 496.5888h164.4032l-164.4032 130.3552v-130.3552z m0-65.792H397.312v35.072H204.1856v-35.072zM416.768 374.9888c-8.1408-23.04-19.9168-42.1888-32.768-57.856v-3.328h65.792a280.5248 280.5248 0 0 0-33.024 61.184zM301.6192 289.28c22.6816 11.0592 95.6928 54.4256 95.6928 153.9072v31.1296H204.1856v-31.1296c0-87.5008 75.1104-140.1856 97.4336-153.9072zM123.6992 839.1168v-23.6032c0-7.2704 3.2768-13.9776 8.9088-18.4832l264.704-209.8688v275.5072H147.2512c-13.0048 0.0512-23.552-10.5472-23.552-23.552z m228.7104 104.2944a17.71008 17.71008 0 0 1-16.9472 12.8h-58.88c-8.2944 0-15.36-5.632-17.2032-13.7216l-11.1616-49.1008H366.592l-14.1824 50.0224z m75.6224-387.9936V480.4608c0-105.1136 60.5184-169.3696 82.5856-189.2864 22.3744 16.4864 80.384 70.7584 80.384 189.2864v382.208h-63.9488V437.4528c0-8.4992-6.8608-15.36-15.36-15.36s-15.36 6.8608-15.36 15.36v425.2672H428.032v-307.3024z m338.8416 387.1232a17.54112 17.54112 0 0 1-17.2032 13.7216h-58.88c-7.8336 0-14.7968-5.2736-16.9472-12.8l-14.1824-50.0224h118.3744l-11.1616 49.1008z m133.4272-103.424c0 13.0048-10.5984 23.6032-23.6032 23.6032h-254.976v-278.3232l199.0144 157.0304 70.6048 55.7056c5.6832 4.5056 8.96 11.264 8.96 18.5344v23.4496z"
            fill="#333333"
            p-id="6439"
          ></path>
        </svg>
      </div>
    </transition> -->

    <div v-if="home_hide" class="home-menus" @touchmove.prevent>
      <div class="home-menus-nav"></div>
      <div
        class="home-menus-back"
        @click="
          home_hide = false;
          move();
        "
      ></div>
    </div>
  </div>
</template>
<style>
@import "../../assets/css/home.css";
</style>
<script>
import logtag from "../../components/tag.vue";
import log_item from "../../components/log-item.vue";
import log_item2 from "../../components/log-item2.vue";
import notice from "../../components/notice.vue";
import new_article from "../../components/new-article.vue";
import classify from "../../components/classify.vue";
import archive from "../../components/archive.vue";
import log_info from "../../components/log-info.vue";
import phone_home from "../../components/phone_home.vue";
import log_nav from "../../components/log-nav.vue";
import log_bottom from "../../components/log-bottom.vue";
import log_card from "../../components/log-card.vue";
import log_nav1 from "../../components/log_nav1.vue";
import music from "../music.vue";
import {mapState} from 'vuex'
export default {
  components: {
    log_item,
    log_item2,
    notice,
    new_article,
    classify,
    logtag,
    archive,
    log_info,
    phone_home,
    log_nav,
    log_bottom,
    log_card,
    log_nav1,
    music,
  },
  data() {
    return {
      //主页面内容左边切换
      currentvue:null,
      nav_show: true,
      home_hide: false,
      rocketshow: false,
      rocketheight: 0,
      // windowWidth: document.documentElement.clientWidth, //实时屏幕宽度
      // windowHeight: document.documentElement.clientHeight, //实时屏幕高度
      oldscrolltop: 0,
      scrollStep:0,
      //log_item测试数据
      log_img_srcs: [
        require("../../assets/img/log-img/20201202-3021.png"),
        require("../../assets/img/log-img/20201210-3029.png"),
        require("../../assets/img/log-img/20201203-3022.png"),
        require("../../assets/img/log-img/20201207-3026.png"),
        require("../../assets/img/log-img/20201206-3025.png"),
        require("../../assets/img/log-img/20201201-3020.png"),
        require("../../assets/img/log-img/20121204-71.png"),
        require("../../assets/img/log-img/20121208-75.png"),
        require("../../assets/img/log-img/20201205-3024.png"),
      ],
      log_info_title: [
        "文章数目:",
        "本站总字数:",
        "本站访客数:",
        "本站总访问量:",
      ],
      log_info_count: ["104", "167.5k", "2", "232"],
      archive_date: [
        "十二月 2020",
        "十一月 2020",
        "十月 2020",
        "九月 2020",
        "八月 2020",
        "七月 2020",
        "六月 2020",
        "五月 2020",
        "四月 2020",
      ],
      archive_count: ["1", "2", "3", "4", "5", "6", "7", "8", "9"],
      log_title: [
        "草泥马的世界1",
        "草泥马的世界2",
        "草泥马的世界3",
        "草泥马的世界4",
        "草泥马的世界5",
        "草泥马的世界6",
        "草泥马的世界7",
        "草泥马的世界8",
        "草泥马的世界9",
        "草泥马的世界10",
      ],
      log_date: [
        "2021-04-01",
        "2021-04-01",
        "2021-04-01",
        "2021-04-01",
        "2021-04-01",
        "2021-04-01",
        "2021-04-01",
        "2021-04-01",
        "2021-04-01",
        "2021-04-01",
        "2021-04-01",
      ],
      log_content: [
        " Reprinted from ONE摄影对自己不满足，是任何真正有天才的人的根本特征之一。摄影我告诉自己，成熟意味着镇静自若地接受生活的波折，要在实际生活和理论之间划出一道界限。",
        " Reprinted from ONE摄影对自己不满足，是任何真正有天才的人的根本特征之一。摄影我告诉自己，成熟意味着镇静自若地接受生活的波折，要在实际生活和理论之间划出一道界限。",
        " Reprinted from ONE摄影对自己不满足，是任何真正有天才的人的根本特征之一。摄影我告诉自己，成熟意味着镇静自若地接受生活的波折，要在实际生活和理论之间划出一道界限。",
        " Reprinted from ONE摄影对自己不满足，是任何真正有天才的人的根本特征之一。摄影我告诉自己，成熟意味着镇静自若地接受生活的波折，要在实际生活和理论之间划出一道界限。",
        " Reprinted from ONE摄影对自己不满足，是任何真正有天才的人的根本特征之一。摄影我告诉自己，成熟意味着镇静自若地接受生活的波折，要在实际生活和理论之间划出一道界限。",
        " Reprinted from ONE摄影对自己不满足，是任何真正有天才的人的根本特征之一。摄影我告诉自己，成熟意味着镇静自若地接受生活的波折，要在实际生活和理论之间划出一道界限。",
        " Reprinted from ONE摄影对自己不满足，是任何真正有天才的人的根本特征之一。摄影我告诉自己，成熟意味着镇静自若地接受生活的波折，要在实际生活和理论之间划出一道界限。",
        " Reprinted from ONE摄影对自己不满足，是任何真正有天才的人的根本特征之一。摄影我告诉自己，成熟意味着镇静自若地接受生活的波折，要在实际生活和理论之间划出一道界限。",
        " Reprinted from ONE摄影对自己不满足，是任何真正有天才的人的根本特征之一。摄影我告诉自己，成熟意味着镇静自若地接受生活的波折，要在实际生活和理论之间划出一道界限。",
        " Reprinted from ONE摄影对自己不满足，是任何真正有天才的人的根本特征之一。摄影我告诉自己，成熟意味着镇静自若地接受生活的波折，要在实际生活和理论之间划出一道界限。",
      ],
      words: [], //字母数组push，pop的载体
      str: "你好世界！", //str初始化
      letters: [], //str分解后的字母数组
      order: 1, //表示当前是第几句话
      windowHeight(val) {
        let that = this;
      
      },
      //浏览器高度
      htmlHeight: {
        height: "300px",
      },
    };
  },
  watch: {
    notice() {
      this.myhide = this.home_hide;
    },
    windowWidth(val) {
      let that = this;
    },
    //监听order值的变化，改变str的内容
    order(old, newV) {
      if (this.order % 4 == 1) {
        this.str = "江南风骨，天水成碧，天教心愿与身违。";
      } else if (this.order % 4 == 2) {
        this.str = "眼睛在为你下雨，心却在为你打伞 ";
      } else if (this.order % 4 == 3) {
        this.str = "做观庭前花开花落，闲看天上云卷云舒。";
      } else {
        this.str = "夜雨染成天水碧。有些人不需要姿态，也能成就一场惊鸿。";
      }
    },
  },
  mounted() {
 
    window.addEventListener("scroll", this.watchScroll);
    window.addEventListener("scroll", this.handleScrollx, true);
    var that = this;
    // <!--把window.onresize事件挂在到mounted函数上-->
    // window.onresize = () => {
    //   return (() => {
    //     window.fullHeight = document.documentElement.clientHeight;
    //     window.fullWidth = document.documentElement.clientWidth;
    //     that.windowHeight = window.fullHeight; // 高
    //     that.windowWidth = window.fullWidth; // 宽
    //   })();
    // };
    //页面初次加载后调用begin()开始动画
    this.begin();
    this.getHtmlHeight();
   
  },
computed:{
...mapState(['windowWidth'])
},
  methods: {
    // //导航栏传值
    // showchangepages:function(data){
    //    this.currentvue=data;
    //    console.log("导航栏的值"+data);
       
    // },
    //滑动时控制导航条的显示
    watchScroll() {
      let scrollTop =
        document.documentElement.scrollTop ||
        document.body.scrollTop ||
        window.pageYOffset;
      // 滚动条滚动的距离
       this.scrollStep = scrollTop - this.oldscrolltop;
      // 更新——滚动前，滚动条距文档顶部的距离
      this.oldscrolltop = scrollTop;

      if (this.scrollStep < 0) {
        this.nav_show = false;
      } else {
        this.nav_show = true;
      }
    },
    //点击下滑到内容
    scroll_bottom: function () {
      let myheaderdiv = this.$refs.kk;
      var myheaderdivHeight = myheaderdiv.offsetHeight;
      scrollTo(0, myheaderdivHeight);
    },
    /***取消滑动限制***/
    move() {
      var mo = function (e) {
        e.preventDefault();
      };
      document.body.style.overflow = ""; //出现滚动条
      document.removeEventListener("touchmove", mo, false);
    },
    home_hide_byvalue(val) {
      (this.home_hide = val),
      console.log(this.home_hide);
      console.log(val);
    },
    //控制火箭的显示隐藏
    handleScrollx() {
      this.rocketheight = window.pageYOffset;
    
      if (this.rocketheight > 200) {
        this.rocketshow = true;
      } else {
        this.rocketshow = false;
      }
    },
    //火箭回到顶部
    // hh() {
    //   window.scrollTo(0, 0);
    // },
    //开始输入的效果动画
    begin() {
      this.letters = this.str.split("");
      for (var i = 0; i < this.letters.length; i++) {
        setTimeout(this.write(i), i * 100);
      }
    },
    //开始删除的效果动画
    back() {
      let L = this.letters.length;
      for (var i = 0; i < L; i++) {
        setTimeout(this.wipe(i), i * 50);
      }
    },
    //输入字母
    write(i) {
      return () => {
        let L = this.letters.length;
        this.words.push(this.letters[i]);
        let that = this;
        /*如果输入完毕，在2s后开始删除*/
        if (i == L - 1) {
          setTimeout(function () {
            that.back();
          }, 2000);
        }
      };
    },
    //擦掉(删除)字母
    wipe(i) {
      return () => {
        this.words.pop(this.letters[i]);
        /*如果删除完毕，在300ms后开始输入*/
        if (this.words.length == 0) {
          this.order++;
          let that = this;
          setTimeout(function () {
            that.begin();
          }, 300);
        }
      };
    },
    //获取浏览器高
    getHtmlHeight() {
      let htmlHeight = window.innerHeight + "px";
      this.$set(this.htmlHeight, "height", htmlHeight);
    },
 
  },
};
</script>
