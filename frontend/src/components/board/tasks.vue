<template>
	<draggable element="span" v-model="list" :options="dragOptions" :move="onMove" @start="isDragging=true" @end="isDragging=false" class="list-group">
		<transition-group type="transition" :name="'flip-list'" class="pa-0">
			<v-card v-for="(element, index) in list" :key="index" color="blue-grey darken-2" class="white--text pa-1 ma-3 list-group-item">
				<v-card-title primary-title>
					<div class="headline">{{element.name}}</div>
				</v-card-title>
				<v-card-actions>
					<v-btn flat dark>Otvori</v-btn>
				</v-card-actions>
			</v-card>
		</transition-group>
	</draggable>
</template>

<script>
import draggable from "vuedraggable";

export default {
	props: ['tasks', 'taskGroupId'],
	data: () => ({
		list: [],
		editable: true,
		isDragging: false,
		delayedDragging: false
	}),
	created () {	
		this.list = this.tasks.map((name, index) => {
			return { name, order: index + 1, fixed: false };
		})
	},
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
		list: function () {
			this.$emit('updateListOfTasks', this.list, this.taskGroupId)
		},
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
	
	name: 'Tasks',
	components: {
		draggable
	}
}
</script>

<style scoped>
.ghost {
  opacity: 0.5;
  background: #c8ebfb;
}
.list-group {
  min-height: 200px;
}
.list-group-item {
  cursor: move;
}
</style>


