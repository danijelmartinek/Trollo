<template>
  <v-container text-xs-center class="pa-0">
    <div v-dragscroll:nochilddrag class="horiz-scroll pa-0 grab-bing">
			
			<v-flex v-for="(group, index) in tasks" :key="index" xs8 md5 class="pa-3 board-column">
				<v-card dark color="secondary" class="pa-1">
					<v-card-title primary-title>
						<div class="headline">{{group.taskGroupName}}</div>
					</v-card-title>

					<Tasks v-bind:taskGroupId='group.taskGroupId' v-bind:tasks='group.tasks' v-on:updateListOfTasks="updateTasks" />

				</v-card>
			</v-flex>

		</div>
  </v-container>
</template>

<script>
import { dragscroll } from 'vue-dragscroll'

import Tasks from './tasks.vue'

export default {
	data: () => ({
		tasks: [
			{
				taskGroupId: 123,
				taskGroupName: "Frontend",
				tasks: 
					[
						"Izgled Aplikacije",
						"REST Api",
						"Registracija i Prijava",
						"Upiti baze podataka",
						"Cookies",
						"UX",
						"Profil Korisnika",
						"Board"
					]
			},
			{
				taskGroupId: 456,
				taskGroupName: "Backend",
				tasks: 
					[
						"Izgled Aplikacije",
						"REST Api",
						"Registracija i Prijava",
						"Upiti baze podataka",
						"Cookies",
						"UX",
						"Profil Korisnika",
						"Board"
					]
			},	
		],
		saveTriggered: false
	}),
	methods: {
		updateTasks: function (updatedList, Id) {
			const list = updatedList
			const updatedGroupId = Id

			this.tasks.forEach( (taskGroup) => {
				if(taskGroup.taskGroupId === updatedGroupId){
					taskGroup.tasks = list
				}
			})

			if(this.saveTriggered === false){
				this.saveTriggered = true
				setTimeout(() => { 
					this.saveTaskList()
				}, 5000)
			}

		},
		saveTaskList() {
			this.saveTriggered = false
			
			console.log(this.tasks)
		}
	},
	
	name: 'Board',
	components: {
		Tasks
	},
	directives: {
		'dragscroll': dragscroll
	}
}
</script>

<style>

.horiz-scroll {
	overflow: hidden;
	white-space: nowrap;
  width: 100%;
	height: 100vh;
  -webkit-overflow-scrolling: touch;
	border-top: 30px solid transparent;
}

.board-column {
  white-space: normal;
	display: inline-block;
	vertical-align: top;
	width: 70%;

	cursor : -webkit-default;
  cursor : -moz-default;
  cursor : -o-default;
  cursor : default;
}

@media only screen and (min-width: 720px) {
  .board-column{
		width: 50%;
	}
}

@media only screen and (min-width: 1200px) {
  .board-column{
		width: 40%;
	}
}

.board-column:active{
	cursor : -webkit-default;
  cursor : -moz-default;
  cursor : -o-default;
  cursor : default;
}

.grab-bing {
  cursor : -webkit-grab;
  cursor : -moz-grab;
  cursor : -o-grab;
  cursor : grab;
}
.grab-bing:active {
  cursor : -webkit-grabbing;
  cursor : -moz-grabbing;
  cursor : -o-grabbing;
  cursor : grabbing;
}
</style>