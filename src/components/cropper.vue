<!--图片裁剪上传组件-->

<template>
  <div>
    <Button type="ghost" icon="ios-cloud-upload-outline" @click="toggleShow">上传图片</Button>
    <!--<a class="btn" @click="toggleShow">设置头像</a>-->
    <my-upload field="file"
               @crop-success="cropSuccess"
               @crop-upload-success="cropUploadSuccess"
               @crop-upload-fail="cropUploadFail"
               v-model="show"
               :width="30"
               :height="30"
               url="/api/admin/file/upload"
               :headers="headers"
               noCircle="true"
               img-format="png"></my-upload>
    <img :src="imgDataUrl">
  </div>
</template>


<script>
  import myUpload from 'vue-image-crop-upload';

  export default {
    data() {
      return {
        show: true,
        imgDataUrl: '' // the datebase64 url of created image
      }
    },
    components: {
      'my-upload': myUpload
    },
    methods: {
      toggleShow() {
        this.show = !this.show;
      },
      /**
       * crop success
       *
       * [param] imgDataUrl
       * [param] field
       */
      cropSuccess(imgDataUrl, field) {
        console.log('-------- crop success --------');
        this.imgDataUrl = imgDataUrl;
      },
      /**
       * upload success
       *
       * [param] jsonData   服务器返回数据，已进行json转码
       * [param] field
       */
      cropUploadSuccess(jsonData, field) {
        console.log('-------- upload success --------');
        console.log(jsonData);
        console.log('field: ' + field);
      },
      /**
       * upload fail
       *
       * [param] status    server api return error status, like 500
       * [param] field
       */
      cropUploadFail(status, field) {
        console.log('-------- upload fail --------');
        console.log(status);
        console.log('field: ' + field);
      }
    }
  }

</script>
