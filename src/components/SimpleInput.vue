<template>
    <div class="card">
      <div class="card-body">
        <div class="input-group mb-3">
          <input type="text" class="form-control" @keyup.enter="trigger" :placeholder="title" aria-label="New peer address" aria-describedby="button-addon2" v-model="searchText">
          <div class="input-group-append">
            <button class="btn btn-primary" ref="sendButton" @click="addPeer" type="button" id="button-addon2">{{submittext}}</button>
          </div>
        </div>
      </div>
    </div>
</template>

<script>
export default {
  name: 'SimpleInput',
   props: {
    title: String,
    submittext: String,
  },
  methods: {
    addPeer(){
      if(this.searchText){
        // console.log(this.searchText)
        this.$emit('new-input',this.searchText)
        this.searchText = ''
      }
    },
    trigger () {
      this.$refs.sendButton.click()
    }
  },
  data(){
    return {
      searchText: ''
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.input-group{
  margin-bottom: 0px !important;
}
</style>
