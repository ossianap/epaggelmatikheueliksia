<template>
	<div class="main">
		<div class="chart-container is-flex is-horizontal-center ">
			<bar-chart 
				v-if="loaded"
				:chart-data="datacollection" 
						:options="options">
			</bar-chart>
		</div>

		<section>
			
			<div class="container">
				<h1 class="title">ΑΥΤΟΚΑΤΕΥΘΥΝΟΜΕΝΗ ΔΙΑΧΕΙΡΙΣΗ ΣΤΑΔΙΟΔΡΟΜΙΑΣ</h1>
				<p>Αυτός ο παράγοντας αφορά το κατά πόσο προσπαθείτε να βασίζεστε στον εαυτό σας για να λάβετε μια απόφαση σχετικά με τη διαμόρφωση των επαγγελματικών σας επιλογών, δέχεστε τη βοήθεια των άλλων και λαμβάνετε υπόψη εξωτερικούς παράγοντες που θα σας βοηθήσουν να πάρετε μια σημαντική απόφαση σχετικά με την επαγγελματική σας σταδιοδρομία.</p> 

				<div>
					<div id="emoji-block" class="is-flex is-horizontal-center">
						<figure class="image is-128x128">
							<img class="purple-theme" src="./../../assets/ads.svg" alt="">
						</figure>
					</div>
					<h2 class="is-size-6 has-text-centered has-text-weight-bold">Το σκορ σου: {{ ads_score }} / 100</h2>
				</div>
			</div>

			
			<div class="container">
				<h1 class="title">ΠΡΟΣΑΝΑΤΟΛΙΣΜΟΣ ΚΑΡΙΕΡΑΣ ΜΕ ΒΑΣΗ ΤΙΣ ΑΞΙΕΣ</h1>
				<p>Αυτός ο παράγοντας αφορά το κατά πόσο μένετε πιστός στις αξίες σας και λαμβάνετε τις αποφάσεις σας με βάσει τις νόρμες και τις αξίες που σας διακατέχουν. Επίσης, το κατά πόσο αξιολογείτε υποκειμενικά την επαγγελματική σας επιτυχία και η επαγγελματική σας σταδιοδρομία διαμορφώνεται από μια σειρά παραγόντων, όπως είναι οι εκπαιδευτικές, οι εργασιακές και οι επαγγελματικές σας εμπειρίας. Τέλος, το κατά πόσο επηρεάζεστε από το επαγγελματικό περιβάλλον και ο πρασανατολισμός της καριέρας και της σταδιοδρομίας προδιαγράφεται με βάση τη συνείδησή σας.</p> 
				<div>
					<div id="emoji-block" class="is-flex is-horizontal-center">
						<figure class="image is-128x128">
							<img class="purple-theme" src="./../../assets/pva.svg" alt="">
						</figure>
					</div>
					<h2 class="is-size-6 has-text-centered has-text-weight-bold">Το σκορ σου: {{ pva_score }} / 100</h2>
				</div>
			</div>
		
			<div class="container">
				<h1 class="title">ΕΠΑΓΓΕΛΜΑΤΙΚΗ ΝΟΟΤΡΟΠΙΑ ΧΩΡΙΣ ΟΡΙΑ ΚΑΙ ΦΥΣΙΚΗ ΚΙΝΗΤΙΚΟΤΗΤΑ</h1>
				<p>Αυτός ο παράγοντας αφορά το κατά πόσο παρουσιάζετε μια ουδέτερη στάση σχετικά με την αναζήτηση ευκαιριών ποικιλομορφίας είτε σε επίπεδο ομάδων εργασίας είτε σε εργασιακό περιβάλλον. Επίσης, το αν είστε αρνητικός σε μια ενδεχόμενη επαγγελματική πρόταση, ωστόσο δεν την επιδιώκετε.</p>
				<div>
					<div id="emoji-block" class="is-flex is-horizontal-center">
						<figure class="image is-128x128">
							<img class="purple-theme" src="./../../assets/eno.svg" alt="">
						</figure>
					</div>
					<h2 class="is-size-6 has-text-centered has-text-weight-bold">Το σκορ σου: {{ eno_score }} / 100</h2>
				</div>
			</div>

		<!-- <section>
			<i>Πηγή: <a href="https://jrounds.weebly.com/onet-interest-profiler-short-form.html">O*NET Interest Profiler Short Form</a></i>
		</section> -->

		</section>

	</div>
</template>

<script>

import IpipChart from './IpipChart.vue'
// import IpipReferenceData from '../../assets/sample_features.json'

var maximumValue = 5;

export default {
	components: {
		'bar-chart': IpipChart
	},
	props: ['formName'],
	data() {
    return {
    //   ipipReference: IpipReferenceData,
			formData: [],
			datacollection : null, 
			loaded: false,
			options:
			{
				scales: {
					yAxes: [
						{
							ticks: {
								suggestedMin:20,
								suggestedMax:100,
								stepSize: 20
							}
						}
					]
				},
				responsive: true,
				maintainAspectRatio: false
			},
		
		}
	},
	async mounted () {
		this.fetchData()
	},
	methods: {
		fetchData() {
			let retrievedFormData = localStorage.getItem('formData');
			this.formData = JSON.parse(retrievedFormData);
			this.fillData();
			this.loaded = true;

			// const database = 'https://open-bigfive-ipip100.firebaseio.com/ipip100/';
			// const id = this.formName;
			// const query = database + id + '.json';
			// this.$http.get(query)
			// 	.then(response => {
			// 		return response.json()
			// 	})
			// 	.then(data => {
			// 		this.formData = data;
			// 		this.fillData();
			// 		this.loaded = true;
			// 	})
		},
		fillData() {
			this.datacollection = {
				labels: ['ΑΥΤΟΚΑΤΕΥΘΥΝΟΜΕΝΗ ΔΙΑΧΕΙΡΙΣΗ ΣΤΑΔΙΟΔΡΟΜΙΑΣ', 
				'ΠΡΟΣΑΝΑΤΟΛΙΣΜΟΣ ΚΑΡΙΕΡΑΣ ΜΕ ΒΑΣΗ ΤΙΣ ΑΞΙΕΣ', 
				'ΕΠΑΓΓΕΛΜΑΤΙΚΗ ΝΟΟΤΡΟΠΙΑ ΧΩΡΙΣ ΟΡΙΑ ΚΑΙ ΦΥΣΙΚΗ ΚΙΝΗΤΙΚΟΤΗΤΑ'],
				datasets: [
					{
						label: 'Το σκορ σου',
						backgroundColor: '#7957d5',
						data: [this.ads_score, this.pva_score, this.eno_score]
					},
			// 		{
			// 			label: 'Μέσος όρος ερωτηθέντων',
			// 			backgroundColor: 'hsl(48, 100%, 67%)',
            // data: [this.ipipReference.f_one.mean,
            //   this.ipipReference.f_two.mean,
            //   this.ipipReference.f_three.mean,
            //   this.ipipReference.f_four.mean,
            //   this.ipipReference.f_five.mean]
			// 		}
				]
			}
		},
		getMultiplier(factor)
		{
			return 100 /
				(this.formData.filter(item => item.factor == factor).length
					* maximumValue)
		},
		getScore(factor)
		{
			return Math.round(this.formData
				.filter(item => item.factor == factor)
				.reduce( (Sum, item) => parseInt(item.value,10) + Sum, 0) * this.getMultiplier(factor))
		}
	},
	computed: {
		ads_score() {
			return this.getScore('ΑΥΤΟΚΑΤΕΥΘΥΝΟΜΕΝΗ ΔΙΑΧΕΙΡΙΣΗ ΣΤΑΔΙΟΔΡΟΜΙΑΣ')
		},
		pva_score() {
			return this.getScore('ΠΡΟΣΑΝΑΤΟΛΙΣΜΟΣ ΚΑΡΙΕΡΑΣ ΜΕ ΒΑΣΗ ΤΙΣ ΑΞΙΕΣ')
		},
		eno_score() {
			return this.getScore('ΕΠΑΓΓΕΛΜΑΤΙΚΗ ΝΟΟΤΡΟΠΙΑ ΧΩΡΙΣ ΟΡΙΑ ΚΑΙ ΦΥΣΙΚΗ ΚΙΝΗΤΙΚΟΤΗΤΑ')
		}
	}
}

</script>

<style scoped>
.main {
	margin-top:30px;
}

.is-horizontal-center {
	justify-content: center;
}

#emoji-block {
	margin-top:2em;
}

.main div.container {
	padding-top: 30px;
}

.purple-theme {
	filter: brightness(0) saturate(100%) invert(54%) sepia(79%) saturate(5539%) hue-rotate(236deg) brightness(89%) contrast(87%);
}
</style>
