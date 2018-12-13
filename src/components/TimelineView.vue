<template>
	<v-app class="timelineView">
		<v-card class="card grey darken-2" max-width tile v-for="(item,index) in timeline" :key="index">
			<v-card-title primary-title>
				<p v-html="item.monologue.replace(/\n/g,'<br/>')">{{item.monologue}}</p>
			</v-card-title>
			<v-card-text>
				<p class="text-xs-right">{{item.date}}</p>
				</v-card-text>
		</v-card>
	</v-app>
</template>

<script>
  export default {
    name: "timelineView",
    data() {
      return {
				timeline: []
			}
		},
		created: function() {
			this.timeline = []
			this.listen()
		},
    methods: {
			listen () {
				firebase.database().ref("monologues/").limitToLast(100).on("value", snapshot => {
					if (snapshot) {
						const rootList = snapshot.val()
						let list = []

						Object.keys(rootList).forEach((val, key) => {
							rootList[val].id = val
							list.push(rootList[val])
						})
						list.reverse()
						this.timeline = list
					}
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
.card{
	margin-top: 10px;
}
</style>