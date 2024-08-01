<template>
  <swiper
      :direction="'vertical'"
      :modules="modules"
      :pagination="{ clickable: true }"
  >
    <!--Cover-->
    <swiper-slide>
      <div class="report-container">
        <div class="title-container">
          <h3>{{year}}</h3>
          <h3>Travel</h3>
          <h3>AnnualReport</h3>
          <h3>年度旅行报告</h3>
        </div>
        <img src="../assets/image/report.gif" id="report-image" alt="Image 2">
        <div class="tips-title"><p>下滑查看更多</p></div>
      </div>
    </swiper-slide>

    <!--Page 1-->
    <swiper-slide>
      <div class="report-container" >
        <img src="../assets/image/map.gif" id="map-image" alt="Image 2">
        <div class="right-text-overlay">
          <p class="right-text-p">这一年<br>
            你一共去了<span class="highlight">{{city_num}}</span>个城市
            <br>超过了<span class="highlight">{{exceed_friend_rate}}</span>的好友
          </p>

          <p class="right-text-p">你旅行目的地偏好<span class="highlight">{{fav_area}}</span><br>
            这里的哪些人、事和景吸引着你呢
          </p>
        </div>
      </div>
    </swiper-slide>

    <!--Page 2-->
   <swiper-slide style="background: linear-gradient(to left, #000000, #6e5995);">
     <div id="report-container">
       <div class="left-text-overlay">
         <p class="left-text-p">你最长时间的一次旅行持续<span class="highlight">{{longest_travel.day_num}}</span>天<br>
           在<span class="highlight">{{longest_travel.month}}</span>月份<br>
           你从<span class="highlight">{{longest_travel.route}}</span><br>
           足足去了<span class="highlight">{{longest_travel.city_num}}</span>个城市<br>
           这一定是一段很难忘的记忆吧
         </p>
       </div>
       <img src="../assets/image/plane.gif" id="plane-image" alt="Image 2">
     </div>
    </swiper-slide>

    <!--Page 3-->
    <swiper-slide>
      <div id="report-container">
        <img src="../assets/image/friend.gif" id="map-image" alt="Image 2">
        <div class="right-text-overlay">
          <p class="right-text-p">{{year}}年<br>
            和你去过最多相同地方的好友是<span class="highlight">{{common_city.friend}}</span><br>
            去过的相同城市数量高达<span class="highlight">{{common_city.city_num}}</span>个<br>
            包括<span class="highlight">{{common_city.city_name}}</span><br>
            旅行偏好这么相似<br>
            下次出发，记得叫上ta哦<br>
          </p>
        </div>
      </div>
    </swiper-slide>

    <!--Page 4-->
    <swiper-slide style="background: linear-gradient(to bottom, #000000, #6e5995);">
     <div id="report-container" >
       <div class="center-text-overlay">
         <p class="center-text-p">
           {{year}}<br>
           你的旅行Blog里出现得最多的词是<br>
           <span class="highlight" style="font-size: 36px">{{blog_preference.word}}</span><br>
           频率高达<span class="highlight" style="font-size: 24px">{{blog_preference.freq}}</span>次
         </p>
       </div>
       <div class="left-text-overlay">
         <p class="left-text-p" v-for="(item, index) in blog_preference.contentWithDate" :key="index">
           <span v-html="highlightWord(item.content, blog_preference.word)"></span> <br>
           &#45;&#45; {{ item.date }}
         </p>
       </div>
       <img src="../assets/image/ticket.gif" id="ticket-image" alt="Image 2">
     </div>
   </swiper-slide  >

    <!--Page 5-->
    <swiper-slide style="background: linear-gradient(to bottom, #000000, #6e5995);">
      <div id="report-container" >
        <div class="left-text-overlay">
          <p class="left-text-p">
            {{special_travel.date}}<span class="highlight">{{special_travel.city}}</span><br>
            大概是很特别的一次旅行吧<br>
            你足足发了<span class="highlight">{{special_travel.blog_num}}</span>条Blog
           ，<span class="highlight">{{special_travel.pic_num}}</span>张照片
            <br>
            遇见了什么让你这么开心呢
          </p>
        </div>
        <img src="../assets/image/camera.gif" id="camera-image" alt="Image">
        <img src="../assets/image/photo.png" id="photo-image" alt="Image">
      </div>
    </swiper-slide>
    
<!--    End Page-->
    <swiper-slide style="background: linear-gradient(to bottom, #000000, #6e5995);">
      <div class="report-container" >
        <div class="title-container">
          <h3>Keep Going</h3>
          <h3>新的一年</h3>
          <h3>继续步履不停吧</h3>
        </div>
        <img src="../assets/image/foot.png" id="foot-image" alt="Image 2">
      </div>
    </swiper-slide>
  </swiper>
</template>

<script setup>
import { ref,reactive } from "vue";
import { Pagination } from "swiper";
import { Swiper, SwiperSlide } from "swiper/vue";
import "../assets/style/report.css";
import "swiper/swiper.min.css";

const year = ref(2024);
const city_num = ref(5);
const exceed_friend_rate = ref("50%");
const fav_area = ref("长三角地区");
const longest_travel = reactive({ day_num: 7, month: 5, route: "扬州-杭州-南京", city_num: 3 });
const common_city = reactive({ friend: "鱼籽酱虾球", city_name: "南京,扬州,杭州...", city_num: 3 });
const blog_preference = reactive({
  word: "轻松拿下",
  freq: 6,
  contentWithDate: [
    { content: "小小泰山，轻松拿下", date: "2024.2.29" },
    { content: "日行三万步，轻松拿下pyq第一名", date: "2024.4.15" },
    { content: "本人已轻松拿下环青海湖骑行，望周知", date: "2024.5.1" }
  ],
});
const special_travel = reactive({
  date: "5月12日",
  city: "长沙",
  blog_num: 5,
  pic_num: 20
});

function highlightWord(content, word) {
  const regex = new RegExp(`(${word})`, 'gi');
  return content.replace(regex, '<span class="highlight">$1</span>');
}

const modules = ref([Pagination]);

</script>

<style scoped>
:deep(.highlight) {
  color: #ffdd00;
}
</style>