<template>
  <v-app dark id="mutterPost">
		<v-container class="PostMonologue" fluid grid-list-md>
      <v-layout align-start justify-center row wrap>
      	<v-flex xs6>
    			<p class="display-2">hitorigoto</p>
					<v-textarea box class="monologueText" height="200" no-resize label="hitorigotoをこぼしてみよう" v-model="monologue"></v-textarea>
					<v-btn large class="addMonologueBtn" @click="addMonologue">Flush this hitorigoto</v-btn>
					<TimelineView></TimelineView>
		    </v-flex>
      </v-layout>
		</v-container>
  </v-app>
</template>

<script>
	import TimelineView from "./TimelineView.vue";
  export default {
		name: "mutterPost",
		components:{
			TimelineView: TimelineView
		},
    data() {
      return {
				monologue: ""
			}
		},
		created: function() {},
    methods: {
			addMonologue: function() {
				if ((this.monologue.length <= 300) && (this.monologue.length > 0)) {
					const date = new Date()
					firebase
						.database()
						.ref("monologues")
						.push({
							monologue: this.monologue,
							date: this.dateTime = (date.getFullYear() + "/" + date.getMonth() + "/" + date.getDate() + " " + date.getHours() + ":" + date.getMinutes() + ":" + date.getSeconds())
						})
					this.monologue = ""
				}else{
					window.alert("hitorigotoは300文字以下で入力してください")
				}
			}
		}
  }
</script>

<style lang="scss" scoped>
.addMonologueBtn {
	margin-top: 15px;
}
h1 {
	margin-top: 10px;
	margin-bottom: 10px;
}
</style>