<template>
    <div id = "statistics_form">
        <section>
            <md-button @click = "active = true" class = "md-raised md-accent md-button-custom">
                Create a post
            </md-button>
            <md-dialog :md-active.sync = "active">
                <md-dialog-title>
                    <b> Share your travel experience! </b>
                </md-dialog-title>
                <md-dialog-content>
                    <div>
                        <md-field>
                            <label> Country</label>
                            <md-select v-model = "post.countryTravelled">
                                <md-option :value = "country" v-bind:key = "country" v-for = "country in country_options_dropdown">
                                    {{country}}
                                </md-option>
                            </md-select>
                        </md-field>
                        <label> Date of Travel Range</label>
                        <md-datepicker :md-disabled-dates = "disabledDatesFrom" md-immediately
                                       v-model = "post.dateTravelled">
                            <label> From</label>
                        </md-datepicker>
                        <md-datepicker :md-disabled-dates = "disabledDatesFrom" md-immediately
                                       v-model = "post.dateTravelledTo">
                            <label> To</label>
                        </md-datepicker>
                        <label> No. of Travellers</label>
                        <md-field>
                            <label>Adult (16+)</label>
                            <md-select v-model = "post.numAdult">
                                <md-option value = "1"> 1</md-option>
                                <md-option value = "2"> 2</md-option>
                                <md-option value = "3"> 3</md-option>
                                <md-option value = "4"> 4</md-option>
                                <md-option value = "5"> 5</md-option>
                                <md-option value = "5++"> 5++</md-option>
                            </md-select>
                        </md-field>
                        <md-field>
                            <label> Child (below 15) </label>
                            <md-select v-model = "post.numChild">
                                <md-option value = "0"> 0</md-option>
                                <md-option value = "1"> 1</md-option>
                                <md-option value = "2"> 2</md-option>
                                <md-option value = "3"> 3</md-option>
                                <md-option value = "4"> 4</md-option>
                                <md-option value = "5"> 5</md-option>
                                <md-option value = "5++"> 5++</md-option>
                            </md-select>
                        </md-field>
                        <md-field>
                            <label> Elder (65+) </label>
                            <md-select v-model = "post.numElder">
                                <md-option value = "0"> 0</md-option>
                                <md-option value = "1"> 1</md-option>
                                <md-option value = "2"> 2</md-option>
                                <md-option value = "3"> 3</md-option>
                                <md-option value = "4"> 4</md-option>
                                <md-option value = "5"> 5</md-option>
                                <md-option value = "5++"> 5++</md-option>
                            </md-select>
                        </md-field>
                        <label> Purpose of Travel</label>
                        <md-field>
                            <md-select v-model = "post.purpose">
                                <md-option value = "business"> Business</md-option>
                                <md-option value = "study"> Study</md-option>
                                <md-option value = "leisure"> Leisure</md-option>
                                <md-option value = "medical"> Medical Care</md-option>
                                <md-option value = "employment"> Employment</md-option>
                                <md-option value = "others"> Others</md-option>
                            </md-select>
                        </md-field>
                        <md-field>
                            <label>What was your experience in the trip?</label>
                            <md-textarea md-autogrow md-counter = "1000" v-model.trim = "post.content"></md-textarea>
                        </md-field>
                        <label> Does any of the traveller have existing medical condition?</label>
                        <md-switch v-model = "post.medical">Yes</md-switch>
                        <div>
                            <label>Overall public health situation</label>
                            <b-input-group name = "rating_1">
                                <b-form-rating icon-clear = "slash-circle"
                                               icon-empty = "heart"
                                               icon-full = "heart-fill"
                                               icon-half = "heart-half"
                                               show-clear
                                               show-value
                                               show-value-max
                                               v-model = "post.rating_value_1"
                                               variant = "danger">
                                </b-form-rating>
                            </b-input-group>
                        </div>
                        <div>
                            <label>Observing of safety measures by the public</label>
                            <b-input-group>
                                <b-form-rating icon-clear = "slash-circle"
                                               icon-empty = "heart"
                                               icon-full = "heart-fill"
                                               icon-half = "heart-half"
                                               show-clear
                                               show-value
                                               show-value-max
                                               v-model = "post.rating_value_2"
                                               variant = "danger">
                                </b-form-rating>
                            </b-input-group>
                        </div>
                        <div>
                            <label>Contact tracing</label>
                            <b-input-group>
                                <b-form-rating icon-clear = "slash-circle"
                                               icon-empty = "heart"
                                               icon-full = "heart-fill"
                                               icon-half = "heart-half"
                                               show-clear
                                               show-value
                                               show-value-max
                                               v-model = "post.rating_value_3"
                                               variant = "danger">
                                </b-form-rating>
                            </b-input-group>
                        </div>
                        <div>
                            <label>Recommendation to travel</label>
                            <b-input-group>
                                <b-form-rating icon-clear = "slash-circle"
                                               icon-empty = "heart"
                                               icon-full = "heart-fill"
                                               icon-half = "heart-half"
                                               show-clear
                                               show-value
                                               show-value-max
                                               v-model = "post.rating_value_4"
                                               variant = "danger">
                                </b-form-rating>
                            </b-input-group>
                        </div>
                        <div>
                            <label>Overall Satisfaction</label>
                            <b-input-group>
                                <b-form-rating icon-clear = "slash-circle"
                                               icon-empty = "heart"
                                               icon-full = "heart-fill"
                                               icon-half = "heart-half"
                                               show-clear
                                               show-value
                                               show-value-max
                                               v-model = "post.rating_value_5"
                                               variant = "danger">
                                </b-form-rating>
                            </b-input-group>
                        </div>
                    </div>
                </md-dialog-content>
                <md-dialog-actions>
                    <md-button @click = "resetForm()" class = "md-raised md-accent"> Reset Form</md-button>
                    <md-button @click = "disableButton()" class = "md-raised md-primary"> Submit</md-button>
                    <md-button @click = "active = false; resetForm()" class = "md-raised"> Cancel
                    </md-button>
                </md-dialog-actions>
            </md-dialog>
        </section>
    </div>
</template>

<script>
	import {mapState} from "vuex";
	import moment from "moment";
	
	export default {
		data() {
			return {
				post: {
					content: '',
					dateTravelled: new Date(),
					dateTravelledTo: new Date(),
					numAdult: "1",
					numChild: "0",
					numElder: "0",
					purpose: '',
					medical: false,
					rating_value_1: 0,
					rating_value_2: 0,
					rating_value_3: 0,
					rating_value_4: 0,
					rating_value_5: 0,
					countryTravelled: ''
				},
				active: false,
				disabledDatesFrom: date => {
					return date > this.today
				}
			}
		},
		computed: {
			...mapState(['userProfile', 'posts', 'country_options_dropdown']),
		},
		methods: {
			createPost() {
				this.$store.dispatch('createPost', {
					content: this.post.content,
					countryTravelled: this.post.countryTravelled,
					dateTravelled: this.post.dateTravelled,
					dateTravelledTo: this.post.dateTravelledTo,
					numAdult: this.post.numAdult,
					numChild: this.post.numChild,
					numElder: this.post.numElder,
					purpose: this.post.purpose,
					medical: this.post.medical,
					rating_value_1: this.post.rating_value_1,
					rating_value_2: this.post.rating_value_2,
					rating_value_3: this.post.rating_value_3,
					rating_value_4: this.post.rating_value_4,
					rating_value_5: this.post.rating_value_5
				})
				this.resetForm()
			},
			disableButton() {
				if (this.post.content === ''
					|| this.post.content === null
					|| this.post.countryTravelled === null
					|| this.post.dateTravelled === null
					|| this.post.purpose === null
					|| this.post.rating_value_1 === null
					|| this.post.rating_value_2 === null
					|| this.post.rating_value_3 === null
					|| this.post.rating_value_4 === null) {
					this.active = true;
					alert("You should fill up all information")
				} else {
					if (this.post.dateTravelled > this.post.dateTravelledTo) {
						alert("The end date of your trip should not be smaller than your start date")
					} else if (this.post.numAdult + this.post.numChild + this.post.numElder === 0) {
						this.active = true;
						alert("There should be at least one person travelling")
					} else {
						console.log("Creating a post")
						this.createPost();
						this.active = false;
						this.resetForm()
					}
				}
			},
			resetForm() {
				this.post.content = null
				this.post.dateTravelled = this.today;
				this.post.dateTravelledTo = this.today;
				this.post.numAdult = 1
				this.post.numChild = 0
				this.post.numElder = 0
				this.post.purpose = null
				this.post.medical = false
				this.post.rating_value_1 = null
				this.post.rating_value_2 = null
				this.post.rating_value_3 = null
				this.post.rating_value_4 = null
                this.post.rating_value_5 = null
				this.post.countryTravelled = null
			},
		},
		filters: {
			formatDate(val) {
				if (!val) {
					return '-'
				}
				let date = val.toDate()
				return moment(date).fromNow()
			},
			formatDateTravelled(val) {
				if (!val) {
					return '-'
				}
				let date = val.toDate()
				return moment(date).format('MMM-DD-YYYY')
			},
			trimLength(val) {
				if (val.length < 200) {
					return val
				}
				return `${val.substring(0, 200)}...`
			}
		},
		created() {
			this.today = new Date();
			this.today.setHours(0, 0, 0, 0);
			this.post.dateTravelled = this.today;
			this.post.dateTravelledTo = this.today;
		}
	}
</script>