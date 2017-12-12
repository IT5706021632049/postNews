<template>
  <div >

      <p class = "bg" style="color : white">BhubejhrCare</p>


    <div id="">
      <div v-show ="showImage">
        <img  :src="image"/>
      </div>
        <input type="file"  @change="onFileChange" />
    </div><br>

    <div class="field">
      <label class="label">หัวข้อ</label>
      <p class="control">
        <textarea v-model="description" rows="2" cols="80" placeholder="Someting about photo"></textarea>
      </p>
    </div>

    <div class="field">
      <label class="label">รายละเอียด</label>
        <p class="control">
          <textarea v-model="comment" rows="2" cols="80" placeholder="Someting about photo"></textarea>
        </p>
    </div>

    <div class="field is-grouped">
        <p class="control">
          <router-link to="/">
            <button class="button is-success is-outlined" @click="addPostToApp($event)">Submit</button>
          </router-link>
        </p>
    </div>

  </div>
</template>

<script>
var image = new Image()
export default {
  props: ['addPost'],
  name: 'hello',
  data () {
    return {
      description: '',
      file: '',
      showImage: false,
      comment: ''
    }
  },
  methods: {
    addPostToApp (e) {
      var newPost = {
        description: this.description,
        comment: this.comment
      }
      this.addPost(newPost, this.file)
      this.comment = ''
      this.description = ''
      this.file = ''
      this.image = ''
      this.showImage = false
    },
    onFileChange (e) {
      var files = e.target.files
      var vm = this
      image = ''
      this.showImage = false
      this.file = files[0]
      var reader = new FileReader()
      reader.onload = function (e) {
        vm.image = e.target.result
        vm.showImage = true
        console.log(this.file)
      }
      reader.readAsDataURL(this.file)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style type="text/css">
.head{
  width: 100%;
  height: 40px;
  display: inline-block;
  background:#00352c;
  box-shadow: 0 0 5px #000;
  position: fixed;
}
.bg{
    background:#00352c;
    width: 100%;
}

</style>
