<script setup lang="ts">
   // 引入reactive函数，用于创建响应式数据
   import { reactive } from "vue";
   // 引入dayjs库，用于处理日期和时间
   import dayjs from "dayjs";
   // 引入DateDataType类型
   import type { DateDataType } from "./index.d";
   // 引入useSettingStore函数，用于获取设置存储
   import { useSettingStore } from "@/stores/index";

   // 创建响应式数据
   const dateData = reactive<DateDataType>({
      dateDay: "",
      dateYear: "",
      dateWeek: "",
      timing: null as any,
   });

   // 获取设置存储
   const { setSettingShow } = useSettingStore();
   // 定义星期数组
   const weekday = ["周日", "周一", "周二", "周三", "周四", "周五", "周六"];
   // 定义时间函数
   const timeFn = () => {
      // 设置定时器，每秒更新一次日期和时间
      dateData.timing = setInterval(() => {
        // 使用dayjs库格式化当前日期和时间
         dateData.dateDay = dayjs().format("YYYY-MM-DD hh : mm : ss");
         // 获取当前星期几，并从星期数组中获取对应的中文名称
         dateData.dateWeek = weekday[dayjs().day()];
      }, 1000);
   };
   // 调用时间函数
   timeFn();
</script>

<template>
   <div class="d-flex jc-center title_wrap">
      <div class="zuojuxing"></div>
      <div class="youjuxing"></div>
      <div class="guang"></div>
      <div class="d-flex jc-center">
         <div class="title">
            <span class="title-text">互联网设备可视化平台</span>
         </div>
      </div>
      <div class="timers">
         {{ dateData.dateYear }} {{ dateData.dateWeek }} {{ dateData.dateDay }}

         <div class="setting_icon" @click="setSettingShow(true)">
            <img src="@/assets/img/headers/setting.png" alt="设置" />
         </div>
      </div>
   </div>
</template>

<style scoped lang="scss">
   .title_wrap {
      height: 60px;
      background-image: url("../assets/img/top.png");
      background-size: cover;
      background-position: center center;
      position: relative;
      margin-bottom: 4px;

      .guang {
         position: absolute;
         bottom: -26px;
         background-image: url("../assets/img/guang.png");
         background-position: 80px center;
         width: 100%;
         height: 56px;
      }

      .zuojuxing,
      .youjuxing {
         position: absolute;
         top: -2px;
         width: 140px;
         height: 6px;
         background-image: url("../assets/img/headers/juxing1.png");
      }

      .zuojuxing {
         left: 11%;
      }

      .youjuxing {
         right: 11%;
         transform: rotate(180deg);
      }

      .timers {
         position: absolute;
         right: 0;
         top: 30px;
         font-size: 18px;
         display: flex;
         align-items: center;

         .setting_icon {
            width: 20px;
            height: 20px;
            cursor: pointer;
            margin-left: 12px;
            img {
               width: 100%;
               height: 100%;
            }
         }
      }
   }
   .title {
      position: relative;
      // width: 500px;
      text-align: center;
      background-size: cover;
      color: transparent;
      height: 60px;
      line-height: 46px;

      .title-text {
         font-size: 38px;
         font-weight: 900;
         letter-spacing: 6px;
         width: 100%;
         background: linear-gradient(
            92deg,
            #0072ff 0%,
            #00eaff 48.8525390625%,
            #01aaff 100%
         );
         -webkit-background-clip: text;
         -webkit-text-fill-color: transparent;
      }
   }
</style>
