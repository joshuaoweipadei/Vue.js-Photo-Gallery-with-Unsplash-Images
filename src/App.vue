<template>
<div id="app">
	<div class="container">
		<div class="row mt-5">
			<div class="col-md-12">
				<div>
					<h3>Vue.js + Unsplash Images - A Pinterest Like-Style Photo Gallery App</h3>
				</div>
				<div class="search mt-3">
					<label>Search for your favourite images</label>
					<form @submit.prevent="searchUnslash(search)" class="d-flex justify-content-between">
						<input type="text" v-model="search" class="form-control" >
						<button type="submit" class="btn btn-primary ml-1"><i class="fa fa-search"></i></button>
					</form>
				</div>
				<div class="mt-5">
					<div v-if="loading" class="text-center">Loading. . .</div>
					<div v-if="images.length < 1 && !loading">No records found</div>
					<stack :column-min-width="300" :gutter-width="15" :gutter-height="15" monitor-images-loaded >
						<stack-item v-for="(image, i) in images" :key="i" style="transition: transform 300ms" >
							<div class="grid-content">
								<img :src="image.urls.small" :alt="image.alt_description" />
								<div class="img-text d-flex justify-content-between align-items-center">
									<span class="small text-capitalize">Desc: {{image.alt_description}}</span>
									<span class="small text-primary">{{image.likes}} <i class="fa fa-heart"></i></span>
								</div>
							</div>
						</stack-item>
					</stack>
				</div>

				<div style="margin-top:100px; margin-bottom:50px; font-size:12px" class="text-center">
					<p class="mb-1">GitHub: <a href="https://github.com/joshuaoweipadei/Vue.js-Photo-Gallery-with-Unsplash-Images">https://github.com/joshuaoweipadei/Vue.js-Photo-Gallery-with-Unsplash-Images</a></p>
					<p>Created by Joshua Oweipadei Bayefa</p>
				</div>
			</div>
		</div>
	</div>
</div>
</template>

<script>
import axios from 'axios';
import { Stack, StackItem } from "vue-stack-grid";

export default {
    name: 'App',
	components: {
		Stack,
		StackItem
	},
	created(){
		this.searchUnslash(this.search)
	},
	data: () => ({
		search: 'cars',
		images: [],
		loading: false
	}),
	methods: {
		searchUnslash(topic){
			this.images = [];
			this.loading = true;
			axios.get(`https://api.unsplash.com/search/photos?query=${topic}&per_page=30`, {
				headers: {
					Authorization: "Client-ID <ENTER_YOUR_UNSPLASH_ACCESS_KEY>",
					"Accept-Version": "v1"
				}
			}).then((res) => {
				this.loading = false;
				this.images = res.data.results;
			}).catch((err) => {
				console.log(err)
				this.loading = false;
				this.images = [];
			});
		}
	}
}
</script>

<style>
*{
	margin: 0px;
	padding: 0px;
}
.grid-content{
	position: relative;
}
.img-text{
	position: absolute;
	bottom: 10px;
	padding: 0px 10px;
	background: #e1e1e1;
	width: 100%;
}
img {
  width: 100%;
  height: auto;
  border-radius: 12px;
}
</style>
