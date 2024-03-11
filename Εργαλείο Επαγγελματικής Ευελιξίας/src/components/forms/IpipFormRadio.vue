<template>
	<div>
		<section>
			<h2 class="subtitle has-text-centered">
				<strong>Πρόοδος</strong>
			</h2>
			<progress class="progress is-warning is-large" :value="countItems" :max="this.questionsNumber">{{ countItems }}</progress>
		</section>

		<section>
			<div v-for="(question, index) in questionnaire" :key="index" class="radioquestion">
				<div :class="{ 'validator-error': question.value != 0 }">

					<div class="box question">
						<h4 class="title is-size-4">{{ index + 1 }} - {{ question.label }}</h4>
						<div class="control">

							<div id="regularcoded">
								<!-- Regular coded options -->
								<div class="columns">
									<div class="column">
										<b-radio v-model="question.value" native-value="1">Διαφωνώ απολύτως</b-radio>
									</div>
									<div class="column">
										<b-radio v-model="question.value" native-value="2">Διαφωνώ εν μέρει</b-radio>
									</div>
									<div class="column">
										<b-radio v-model="question.value" native-value="3">Δε συμφωνώ, ούτε διαφωνώ</b-radio>
									</div>
									<div class="column">
										<b-radio v-model="question.value" native-value="4">Συμφωνώ εν μέρει</b-radio>
									</div>
									<div class="column">
										<b-radio v-model="question.value" native-value="5">Συμφωνώ απόλυτα</b-radio>
									</div>
								</div>
							</div>
						</div>
					</div>
				</div>
			</div>
		</section>

		<section>
			<center>
				<div v-if="countItems >= 1">
					<br>
					<b-button type="is-primary" size="is-large" @click="submit">Αξιολογήστε την ευελιξία μου</b-button>
				</div>
			</center>
		</section>
	</div>


</template>

<script>
export default {
	props: ['questionnaire', 'countItems'],
	methods: {
		submit() {
			localStorage.setItem('formData', JSON.stringify(this.questionnaire));
			this.$emit('sendId', 1234); //random formId for testing

			// this.$http.post('https://open-bigfive-ipip100.firebaseio.com/questionnaire.json', this.questionnaire)
			// 	.then(response => {
			// 		const formId = response.body.name;
			// 		this.$emit('sendId', formId);
			// 	}, error => {
			// 	});
		}
	}
};
</script>

<style scoped>
div {
	margin-top: 1em;
}

.question {
	margin-top: 1em !important;
}

.validator-error {
	border-radius: 6px;
	-webkit-box-shadow: 0 1px 2px #7957d5, 0 0 0 1px #7957d5!important;
	box-shadow: 0 1px 2px #7957d5, 0 0 0 1px #7957d5!important;
}

</style>
