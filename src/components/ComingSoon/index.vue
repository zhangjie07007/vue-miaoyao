<template>
  <div class="movie_body">
    <Loading v-if="isLoading" />
    <Scroller v-else>
      <ul>
        <li v-for="item in movelist" :key="item.id" @touchstart = "todail(item.id)">
          <div class="pic_show">
            <img :src="item.img | filter" />
          </div>
          <div class="info_list">
            <h2>{{item.nm}}</h2>
            <p>
              <span class="person">{{item.wish}}</span> 人想看
            </p>
            <p>主演: {{item.star}}</p>
            <p>{{item.showInfo}}</p>
          </div>
          <div class="btn_pre">预售</div>
        </li>
      </ul>
    </Scroller>
  </div>
</template>

<script>
import { getcomesoon } from "../../api";
export default {
  data() {
    return {
      isLoading: true,
      movelist: []
    };
  },
  name: "ComingSoon",
  mounted() {
    getcomesoon().then(res => {
    //   console.log(res.data.data.comingList);
      this.movelist = res.data.data.comingList;
      this.isLoading = false;
    });
  },
  filters: {
    filter(input) {
      let str = input.replace("w.h", "200.300");
      // console.log(str);
      return str;
    }
  },
  methods:{
      todail(id){
        //   console.log(id)
          this.$router.push(`/movie/dail1/${id}`)
      }
  }
};
</script>






















<style scoped>
#content .movie_body {
  flex: 1;
  overflow: auto;
}
.movie_body ul {
  margin: 0 12px;
  overflow: hidden;
}
.movie_body ul li {
  margin-top: 12px;
  display: flex;
  align-items: center;
  border-bottom: 1px #e6e6e6 solid;
  padding-bottom: 10px;
}
.movie_body .pic_show {
  width: 64px;
  height: 90px;
}
.movie_body .pic_show img {
  width: 100%;
}
.movie_body .info_list {
  margin-left: 10px;
  flex: 1;
  position: relative;
}
.movie_body .info_list h2 {
  font-size: 17px;
  line-height: 24px;
  width: 150px;
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}
.movie_body .info_list p {
  font-size: 13px;
  color: #666;
  line-height: 22px;
  width: 200px;
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}
.movie_body .info_list .grade {
  font-weight: 700;
  color: #faaf00;
  font-size: 15px;
}
.movie_body .info_list img {
  width: 50px;
  position: absolute;
  right: 10px;
  top: 5px;
}
.movie_body .btn_mall,
.movie_body .btn_pre {
  width: 47px;
  height: 27px;
  line-height: 28px;
  text-align: center;
  background-color: #f03d37;
  color: #fff;
  border-radius: 4px;
  font-size: 12px;
  cursor: pointer;
}
.movie_body .btn_pre {
  background-color: #3c9fe6;
}
</style>
