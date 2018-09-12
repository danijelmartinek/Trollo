<template>
  <v-container text-xs-center class="pa-0">
    <div v-dragscroll:nochilddrag class="horiz-scroll pa-0 grab-bing">
			
			<v-flex xs8 md5 class="pa-3 board-column">
        <v-card dark color="secondary" class="pa-1">
					<v-card-title primary-title>
						<div class="headline">Frontend</div>
					</v-card-title>

					<draggable element="span" v-model="list" :options="dragOptions" :move="onMove" @start="isDragging=true" @end="isDragging=false" class="list-group">
						<transition-group type="transition" :name="'flip-list'" class="list-group pa-0">
							<v-card v-for="element in list" :key="element.order" color="blue-grey darken-2" class="white--text pa-1 ma-3 list-group-item">
								<v-card-title primary-title>
									<div class="headline">{{element.name}}</div>
								</v-card-title>
								<v-card-actions>
									<v-btn flat dark>Otvori</v-btn>
								</v-card-actions>
							</v-card>
						</transition-group>
					</draggable>

        </v-card>
      </v-flex>

			<v-flex xs8 md5 class="pa-3 board-column">
        <v-card dark color="secondary" class="pa-1">
					<v-card-title primary-title>
						<div class="headline">Frontend</div>
					</v-card-title>

					<draggable element="span" v-model="list2" :options="dragOptions" :move="onMove" class="list-group">
						<transition-group name="no" tag="ul" class="list-group pa-0">
							<v-card v-for="element in list2" :key="element.order" color="blue-grey darken-2" class="white--text pa-1 ma-3 list-group-item">
								<v-card-title primary-title>
									<div class="headline">{{element.name}}</div>
								</v-card-title>
								<v-card-actions>
									<v-btn flat dark>Otvori</v-btn>
								</v-card-actions>
							</v-card>
						</transition-group>
					</draggable>

        </v-card>
      </v-flex>

			<v-flex xs8 md5 class="pa-3 board-column">
        <v-card dark color="secondary" class="pa-1">
					<v-card-title primary-title>
						<div class="headline">Database</div>
					</v-card-title>

					<draggable element="span" v-model="list3" :options="dragOptions" :move="onMove" class="list-group">
						<transition-group name="no" tag="ul" class="list-group pa-0">
							<v-card v-for="element in list3" :key="element.order" color="blue-grey darken-2" class="white--text pa-1 ma-3 list-group-item">
								<v-card-title primary-title>
									<div class="headline">{{element.name}}</div>
								</v-card-title>
								<v-card-actions>
									<v-btn flat dark>Otvori</v-btn>
								</v-card-actions>
							</v-card>
						</transition-group>
					</draggable>

        </v-card>
      </v-flex>

		</div>
  </v-container>
</template>

<script>
	import { dragscroll } from 'vue-dragscroll'
	import draggable from "vuedraggable";

	const message = [
		"Izgled Aplikacije	",
		"REST Api",
		"Registracija i Prijava",
		"Upiti baze podataka",
		"Cookies",
		"UX",
		"Profil Korisnika",
		"Board"
	];

  export default {
    data: () => ({
      list: message.map((name, index) => {
        return { name, order: index + 1, fixed: false };
      }),
      list2: [],
			list3: [],
      editable: true,
      isDragging: false,
      delayedDragging: false
    }),
		methods: {
			orderList() {
				this.list = this.list.sort((one, two) => {
					return one.order - two.order;
				});
			},
			onMove({ relatedContext, draggedContext }) {
				const relatedElement = relatedContext.element;
				const draggedElement = draggedContext.element;
				return (
					(!relatedElement || !relatedElement.fixed) && !draggedElement.fixed
				);
			}
		},
		computed: {
			dragOptions() {
				return {
					animation: 0,
					group: "description",
					disabled: !this.editable,
					ghostClass: "ghost",
					delay:300,
				};
			},
			listString() {
				return JSON.stringify(this.list, null, 2);
			},
			list2String() {
				return JSON.stringify(this.list2, null, 2);
			}
		},
		watch: {
			isDragging(newValue) {
				if (newValue) {
					this.delayedDragging = true;
					return;
				}
				this.$nextTick(() => {
					this.delayedDragging = false;
				});
			}
		},
    
    name: 'Board',
    components: {
			draggable
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

.ghost {
  opacity: 0.5;
  background: #c8ebfb;
}
.list-group {
  min-height: 20px;
}
.list-group-item {
  cursor: move;
}

.klasa{
  width: 200px;
  height: 10px;
}
</style>