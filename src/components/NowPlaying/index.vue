<template>
  <div class="movie_body" ref="movie_body">
    <Loading v-if="isLoading" />
    <Scroller>
      <ul>
        <li v-for="item in movielist" :key="item.id"  @touchstart="tapHandle(item.id)">
          <div class="pic_show">
            <img :src="item.img | filter" />
          </div>
          <div class="info_list">
            <h2>{{item.nm}}</h2>
            <p>
              观众评
              <span class="grade">{{item.sc}}</span>
            </p>
            <p>主演: {{item.star}}</p>
            <p>{{item.showInfo}}</p>
          </div>
          <div class="btn_mall">购票</div>
        </li>
      </ul>
    </Scroller>
  </div>
</template>

<script>
//import BScroll from 'better-scroll';
import { getplaying } from "../../api";
export default {
  data() {
    return {
      isLoading: true,
      movielist: []
    };
  },
  name: "NowPlaying",
  mounted() {
    if (localStorage.getItem("movielist")) {
      this.movielist = JSON.parse(localStorage.getItem("movielist"));
    } else {
      getplaying().then(res => {
        console.log(res.data.data.movieList);
        this.movielist = res.data.data.movieList;
        localStorage.setItem("movelist", JSON.stringify(this.movielist));
        this.isLoading = false;
      });
    }
  },
  methods: {
    tapHandle(id) {
      this.$router.push(`/movie/dail/${id}`);
    }
  },
  filters: {
    filter(input) {
      let str = input.replace("w.h", "200.300");
      // console.log(str);
      return str;
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
  background-color: #2f8caa;
  color: #fff;
  border-radius: 4px;
  font-size: 12px;
  cursor: pointer;
}
.movie_body .btn_pre {
  background-color: #3faed2;
}
.movie_body .pullDown {
  margin: 0;
  padding: 0;
  border: none;
}
</style>
