<template>
    <div id="main">
        <Header title="喵眼电影" />
            <div id="content">
                <swiper class="swiper"></swiper>
                <div class="movie_menu">
                    <router-link tag="div" to="/movie/city" class="city_name">
                        <span>{{ $store.state.city.nm }}</span><i class="iconfont icon-lower-triangle"></i>
                    </router-link>
                    <div class="hot_swtich">
                        <router-link tag="div" to="/movie/nowPlaying" class="hot_item">正在热映</router-link>
                        <router-link tag="div" to="/movie/comingSoon" class="hot_item">即将上映</router-link>
                    </div>
                    <router-link tag="div" to="/movie/search" class="search_entry">
                        <i class="iconfont icon-sousuo"></i>
                    </router-link>
                    
                </div>
                <keep-alive>
                    <router-view />
                </keep-alive>
            </div>
        <TabBar />
        <router-view name="detail" />
    </div>
</template>

<script>

import Header from '@/components/Header';
import TabBar from '@/components/TabBar';
import swiper from '@/components/swiper'
import { messageBox } from '@/components/JS';

export default {
    name : 'Movie',
    components : {
        Header,
        TabBar,
        swiper
    },
    mounted(){
       
    }
}
</script>

<style scoped>
#content .movie_menu{ width: 100%; height: 45px; border-bottom:1px solid #e6e6e6; display: flex; justify-content:space-between; align-items:center; background:white; z-index:10;}
.movie_menu .city_name{ margin-left: 20px; height:100%; line-height: 45px;}
.movie_menu .city_name.active{ color: #3faed2; border-bottom: 2px #3faed2 solid;}
.movie_menu .city_name.router-link-active{ color: #3faed2; border-bottom: 2px #3faed2 solid;}
.movie_menu .hot_swtich{ display: flex; height:100%; line-height: 45px;}
.movie_menu .hot_item{ font-size: 15px; color:#666; width:80px; text-align:center; margin:0 12px; font-weight:700;}
.movie_menu .hot_item.active{ color: #3faed2; border-bottom: 2px #3faed2 solid;}
.movie_menu .hot_item.router-link-active{ color: #3faed2; border-bottom: 2px #3faed2 solid;}
.movie_menu .search_entry{ margin-right:20px; height:100%; line-height: 45px;}
.movie_menu .search_entry.active{ color: #3faed2; border-bottom: 2px #3faed2 solid;}
.movie_menu .search_entry.router-link-active{ color: #3faed2; border-bottom: 2px #3faed2 solid;}
.movie_menu .search_entry i{  font-size:24px; color:#3faed2;}
.swiper{width: 100%}
.slide-enter-active{ animation : 13s detailMove;}
@keyframes detailMove{
	0%{
		transform : translateX(100%);
	}
	100%{
		transform : translateX(0);
	}
}
</style>
