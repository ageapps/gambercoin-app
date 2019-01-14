<template>
    <div class="card">
      <div class="card-body">
        <div class="input-group mb-3">
          <div v-show="isprivate" class="input-group-prepend">
            <button @click="toggleDropdown" class="btn btn-outline-secondary dropdown-toggle" type="button" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">{{selectedHop}}</button>
            <div v-bind:style="{ display: dropdownDisplay }" class="dropdown-menu">
              <a v-for="(peer,key) in peers" :key = "key" class="dropdown-item" @click="selectNode(key)" >
              {{key}}
              </a>
            </div>
          </div>
          <input type="text" class="form-control" @keyup.enter="trigger" :placeholder="title" aria-label="Recipient's username" aria-describedby="button-addon2"  v-model="newMessage">
          <div class="input-group-append">
            <button class="btn btn-outline-secondary" ref="sendButton" @click="addMessage" type="button" id="button-addon2">Send</button>
          </div>
        </div>


      </div>
    </div>
</template>

<script>
export default {
  name: 'NewMessageInput',
  props: {
    title: String,
    peers: Object,
    isprivate: {
      type: Boolean,
      default: false
    }
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
    trigger () {
      this.$refs.sendButton.click()
    },
    addMessage(){
      if(this.newMessage){
        var data ={
          message: this.newMessage,
        }
        if (this.isprivate){
          data.destination = this.destination;
        }
        this.$emit('new-message', data)
        this.newMessage = ''
        this.destination = ''
      }
    }
  },
  data(){
    return {
      newMessage: '',
      destination: '',
      dropdownDisplay: 'none',
      selectedHop: 'Peers'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
