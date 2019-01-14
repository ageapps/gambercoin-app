<template>
    <div class="card">
      <div class="card-body">
        <div class="input-group mb-3">
          <div class="input-group">
            <button @click="toggleDropdown" class="btn btn-outline-secondary dropdown-toggle" type="button" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">{{selectedHop}}</button>
            <div v-bind:style="{ display: dropdownDisplay }" class="dropdown-menu">
              <a v-for="(peer,key) in peers" :key = "key" class="dropdown-item" @click="selectNode(key)" >
              {{key}}
              </a>
            </div>
          </div>
          <input type="text" class="form-control" :placeholder="title" aria-label="Recipient's username" aria-describedby="button-addon2"  v-model="requestHash">
          <div class="input-group">
            <input type="text" class="form-control" placeholder="File name" aria-label="File name" aria-describedby="button-addon2" v-model="fileName">
          </div>
          <button class="btn btn-outline-secondary" @click="sendRequest" type="button" id="button-addon2">Send</button>
        </div>


      </div>
    </div>
</template>

<script>
export default {
  name: 'NewRequestInput',
  props: {
    title: String,
    peers: Object,
  },
  methods: {
    selectNode(peer){
      this.selectedHop = peer;
      this.destination = peer;
      this.toggleDropdown();
    },
    toggleDropdown(){
      this.dropdownDisplay = this.dropdownDisplay == 'none' ? 'block' : 'none'
    },
    sendRequest(){
      if(this.fileName && this.requestHash && this.destination){
        var data ={
          fileName: this.fileName,
          requestHash: this.requestHash,
          destination: this.destination,
        }
        this.$emit('new-request', data)
        this.requestHash = ''
        this.fileName = ''
        this.destination = ''
      }
    }
  },
  data(){
    return {
      fileName: '',
      requestHash: '',
      destination: '',
      dropdownDisplay: 'none',
      selectedHop: 'Peers'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.btn, .dropdown-menu{
  width: 100%;
}
</style>
