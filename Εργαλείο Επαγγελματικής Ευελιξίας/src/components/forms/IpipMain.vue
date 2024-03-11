<template>
	<div>
		<div class="container">

			<div class="main-title"></div>
			<h1 class="title has-text-centered">Τεστ επαγγελματικής ευελιξίας</h1>
			<!-- <h2 class="subtitle has-text-centered">
				<em>O*NET Interest Profiler - RIASEC interests</em>
			</h2> -->
			<Instructions />
		</div>

		<div class="main-application">
			<b-tabs type="is-toggle"  v-model="activeTab" expanded>
				<b-tab-item label="Τεστ" icon="google-photos">
					<Test :questionnaire="questionnaire_shuffled"
								:countItems="countItems"
								v-on:sendId="fillFormId"/>
				</b-tab-item>

				<b-tab-item label="Αποτελέσματα" icon="library-music">

			<div v-if="!!formName && countItems == this.questionsNumber">
				<Results :formName="formName"/>
			</div>

			<div v-else >
				<div id="emoji-block" class="is-flex is-horizontal-center">
					<figure class="image is-128x128">
						<img src="./../../assets/1f62c.svg" alt="">
					</figure>
				</div>
				<br>
				<h1 class="title has-text-centered">Δε ξεχνάς κάτι;</h1>
				<h2 class="is-size-3 has-text-weight-medium has-text-centered">Λείπουν {{ this.questionsNumber - countItems }} ερωτήσεις.</h2>
				<h2 class="subtitle has-text-centered">Δεν έχεις απαντήσει ακόμη σε όλες τις ερωτήσεις.</h2>
			</div>

			</b-tab-item>

			</b-tabs>
		</div>
	</div>
</template>

<script>
import Test from './IpipFormRadio.vue'
import Instructions from './IpipInstructions.vue'
import Results from './IpipResults.vue'

import questionnaire from '../../assets/questionnaire.json'
var questionnaire_shuffled = shuffle(questionnaire)


function shuffle(sourceArray) {
    for (var i = 0; i < sourceArray.length - 1; i++) {
        var j = i + Math.floor(Math.random() * (sourceArray.length - i));

        var temp = sourceArray[j];
        sourceArray[j] = sourceArray[i];
        sourceArray[i] = temp;
    }
    return sourceArray;
}


function convertToAnswered(value){
	return value > 0 ? 1 : 0;
}

export default {
	components: {
		Test,
		Instructions,
		Results,
	},
	data() {
		return {
			questionnaire_shuffled,
			formName: null,
			activeTab: 0,
			filledForm: this.countItems,
		}
	},
	methods: {
		fillFormId(formId) {
			this.formName = formId;
			this.activeTab = 1;
		},
	},
	computed: {
		countItems() {
			return this.questionnaire_shuffled
				.map(item => convertToAnswered(item.value))
				.reduce( (Sum, item) => item + Sum, 0)
		},
	},
}
</script>

<style scoped>
.question {
	margin-top: 2em
}

.main-application {
	padding-top: 1.5em;
}

.main-title {
	margin-top: 3em;
}

.is-horizontal-center {
	justify-content: center;
}

#emoji-block {
	margin-top:2em;
}

</style>
