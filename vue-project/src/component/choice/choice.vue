<template>
	<div>
		<mt-spinner type="triple-bounce" :size="60" v-show="$store.state.switchShow"  color="#26a2ff" class="order_spinner">
        </mt-spinner>
		<div id="choice">
			<div class="choice_header">
				<h1>优选</h1>
			</div>
			<div class="choice_main" v-show="!$store.state.switchShow">
				<div class="item_detail" v-for="item in hotHotel" v-if="item.hot == 1" @click="toDetail(item.id)">
					<div class="pic">
						<img v-lazy= "item.image1" />
					</div>
					<div class="bottom">
						<div class="left">
							<p class="hotelName">{{item.hotelName}}</p>
							<p class="enName">{{item.enghotelName}}</p>
						</div>
						<div class="right">
							￥2，487起
						</div>	
					</div>				
				</div>
			</div>
		</div>
		<footernav></footernav>
	</div>
</template>

<script>
	import "./choice.scss";
	import footernav from "../footernav/footernav.vue";
	import http from "../../http/baseUrl.js";
	
	export default {
		data(){
			return {
				hotHotel:[]
			}
		},
		components:{
			footernav
		},
		beforeMount(){
			this.axios.get(http.url + "/hotHotel").then(res =>{
				this.hotHotel = res.data.data.results;
				this.$store.state.switchShow=false;
				
			})
		},
		methods:{

			toDetail(_id){

				this.$router.push({path:"/detail",query:{id:_id}})

			}
		}
	}
	
</script>

<style>	
	.pic img[lazy=loading] {
	 background-size: cover;
	}

</style>
