<template>
  <div class="connectedUser__container">
    <div class="ui items">
      <div class="item">
        <div class="ui mini image">
          <img :src="currentUser.photoURL" alt="아바타">
        </div>
        <div class="middle aligned content">
          <div class="ui container">
            <div class="ui inverted header">
              {{ currentUser.displayName }}
            </div>
          </div>
        </div>
        <div class="extra">
          <button class="ui circular icon right floated button" @click="logout">
            <i class="icon sign out"></i>
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'

export default {
  name: 'connected-user',
  data () {
    return {
      presenceRef: firebase.database().ref('presence')
    }
  },
  computed: {
    ...mapGetters(['currentUser'])
  },
  methods: {
    logout () {
      this.presenceRef.child(this.currentUser.uid).remove()
      firebase.auth().signOut()
      this.$store.dispatch("setUser", null)
      this.$router.push('/login')
    }
  }
}
</script>

<style scoped>
.connectedUser__container{
  position: absolute;
  background-color: #008066;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  height: 90px;
  padding: 8px;
  box-shadow: -4px 1px 8px 3px #cce6ff;
}
</style>
