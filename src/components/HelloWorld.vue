<template>
  <div class="hello">
    <div class="cropper">
    	<vueCropper
				ref="cropper"
				:img="example2.img"
				:outputSize="example2.size"
				:outputType="example2.outputType"
				:info="example2.info"
				:canScale="example2.canScale"
				:autoCrop="example2.autoCrop"
				:autoCropWidth="example2.autoCropWidth"
				:autoCropHeight="example2.autoCropHeight"
				:fixed="example2.fixed"
				:fixedNumber="example2.fixedNumber"
			></vueCropper>
    </div>
    <div class="test-buttons">
    	<button @click="finish('base64')" class="btn">preview(base64)</button>
			<button @click="finish('blob')" class="btn">preview(blob)</button>
    </div>
  </div>
</template>

<script>
	import vueCropper from 'vue-cropper'

export default {
  name: 'HelloWorld',
  data () {
    return {
			example2: {
				img: 'http://ofyaji162.bkt.clouddn.com/bg1.jpg',
				info: true,
				size: 1,
				outputType: 'jpeg',
				canScale: false,
				autoCrop: true,
				// 只有自动截图开启 宽度高度才生效
				autoCropWidth: 300,
				autoCropHeight: 250,
				// 开启宽度和高度比例
				fixed: true,
				fixedNumber: [4, 3]
			}
		}
  },
  methods:{
  	finish(type){
  	// 输出
			var test = window.open('about:blank')
			test.document.body.innerHTML = '图片生成中..'
			if (type === 'blob') {
				this.$refs.cropper.getCropBlob((data) => {
					var test = window.open('')
					test.location.href = window.URL.createObjectURL(data)
				})
			} else {
				this.$refs.cropper.getCropData((data) => {
					test.location.href = data
				})
			}
  	},
  },
  components: {
		vueCropper
	}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.cropper{
	width: 500px;
	height:500px;
}
</style>
