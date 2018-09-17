<template>
  <v-container text-xs-center class="pa-0">
    <div v-dragscroll:nochilddrag class="pa-0 grab-bing horiz-scroll">

			<v-flex 
				v-for="(group, index) in tasks"
				:key="index"
				xs8 md5
				class="pa-3 board-column"
			>
				<v-card 
					dark
					color="secondary"
					class="pa-1"
				>
					<v-card-title primary-title>
						<div class="headline">{{group.taskGroupName}}</div>
					</v-card-title>

					<Tasks 
						v-bind:taskGroupId='group.taskGroupId'
						v-bind:tasks='group.tasks'
						v-bind:taskCategory='group.taskCategory'
						v-on:updateListOfTasks="updateTasks"
					>
					</Tasks>

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
				taskCategory: 'webdev',
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
				taskCategory: 'webdev',
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
			}
		],
		saveTriggered: false
	}),
	methods: {
		updateTasks: function (updatedList, Id) {
			/**
			 * Looping through `tasks` array to find matching list via updatedGroupId. When founded, matching list in array updates.
			 * At the same time, function triggers `setTimeout()` in which there is another function in charge for sending data to backend.
			 * Before triggering countdown, function checks whether the countdown is already triggered with `this.saveTriggered` variable.
			 * This limits requests to backend to one within 5 seconds when user updates list.
			 * 
			 * @param {Object[]} this.tasks - Groups with list of tasks.
			 * @param {string} list - Updated list from `tasks` array received from `tasks.vue` component.
			 * @param {number} updatedGroupId - Id of received list.
			 * @param {boolean} saveTriggered - To check if `saveTaskList()` function is already triggered whithin last 5 seconds.
			 * 
			 * @function saveTaskList() - Function that triggers PUT method.
			*/

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
