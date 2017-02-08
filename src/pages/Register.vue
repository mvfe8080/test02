<template>
  <div id="app">
    <md-dialog md-open-from="#fab" md-close-to="#fab" ref="dialog2">
      <md-dialog-title>회원가입</md-dialog-title>

      <md-dialog-content>
        <form>
          <md-input-container>
            <label>이름</label>
            <md-textarea placeholder="이름을 입력해 주세요" maxlength="20" name="name" v-model="name"></md-textarea>
          </md-input-container>

          <md-input-container>
            <label>이메일</label>
            <md-input maxlength="20" name="email" v-model="email"></md-input>
          </md-input-container>

          <md-input-container>
            <label>패스워드</label>
            <md-input maxlength="20" name="password" v-model="password"></md-input>
          </md-input-container>

          <md-input-container>
            <label>패스워드확인</label>
            <md-input maxlength="20" name="password_confirmation" v-model="password_confirmation"></md-input>
          </md-input-container>
        </form>
      </md-dialog-content>

      <md-dialog-actions>
        <md-button class="md-primary" @click.prevent="register">회원가입</md-button>
        <md-button class="md-primary" @click="closeDialog('dialog2')">취소</md-button>
        <md-button class="md-primary" @click="closeDialog('dialog2')">가입</md-button>
        <router-link to="/login"><md-button class="md-primary">로그인</md-button></router-link>
      </md-dialog-actions>
    </md-dialog>

    <md-button class="md-fab md-fab-bottom-right" id="fab" @click="openDialog('dialog2')">
      <md-icon>account_box</md-icon>
    </md-button>
  </div>
</template>

<script>
export default {
  name: 'register',
  data () {
    return {
      name: '',
      email: '',
      password: '',
      password_confirmation: ''
    }
  },
  methods: {
    openDialog(ref) {
      this.$refs[ref].open();
    },
    closeDialog(ref) {
      this.$refs[ref].close();
    },
    onOpen() {
      console.log('Opened');
    },
    onClose(type) {
      console.log('Closed', type);
    },
    register () {
      console.log("회원가입");
      firebase.auth().createUserWithEmailAndPassword(this.email, this.password)
      .then( user => {
        console.log("회원가입" + user.email);
      }).catch( error => {
        console.log(error);
      })
    }
  }
};
</script>

<style scoped>

</style>
