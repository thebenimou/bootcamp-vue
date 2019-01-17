<template>
	<div id="app">
		<link rel="stylesheet" :href="css" /> <img class="imagecover" :src="coverimage" />
		<link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet" />
		<div class="container">
			<img class="logo center-align" src="./assets/icon-left-font.svg" />
			<h5>Hi {{ prenom }} 🤓 ! <br />Want to attend great meetups in Paris ?</h5>
			<br />ici un call to action Yes let's go !

			<transition name="fade">
				<div v-if="bloc1_prenom">
					<label>Quel est ton prénom ?</label>
					<input
						type="text"
						v-model="prenom"
						placeholder="indiquez votre prénom"
						@keyup.enter="passer_etape2();"
					/>
					<button
						class="btn waves-effect waves-light "
						@click="passer_etape2();"
						type="submit"
						name="action"
						v-if="prenom.length >= 3"
					>
						Suivant <i class="material-icons right">send</i>
					</button>
				</div>
			</transition>

			<div v-if="exemplesansvfor">
				<div v-if="prenom.length >= 3">
					<label>Quel est votre poste ?</label>
					<select class="browser-default" v-model="jobSelected">
						<option value="" disabled selected>Sélectionner une option</option>
						<option value="Agile consultant">Agile consultant</option>
						<option value="Biz Consultant">Biz Consultant</option>
						<option value="Data">Data</option>
					</select>
					{{ jobSelected }}
				</div>
			</div>

			<transition name="fade">
				<div v-if="bloc2_information && jobSelected === ''">
					<div>
						<label>Enchanté {{ prenom }}, quel est ton sujet du moment ?</label>
						<select class="browser-default" v-model="jobSelected">
							<option value="" disabled selected>Sélectionner une option</option>
							<option v-for="job in jobList" :value="job">{{ job }}</option>
						</select>
						{{ jobSelected }}
					</div>
				</div>
			</transition>

			<transition name="fade">
				<div v-if="jobSelected">
					<label>{{ prenom }}, voici quelques suggestions de meetups :</label>
				</div>
			</transition>

			<transition name="fade">
				<ul v-if="jobSelected != ''">
					<li v-for="event in events">
						<a :href="event.link" target="_blank">Lien du meetup</a>
					</li>
				</ul>
			</transition>

			<br v-for="i in 10" />
			todo : se renseigner là-dessous
			https://stackoverflow.com/questions/15929141/margin-top-not-working-with-label voir
			https://secure.meetup.com/meetup_api
		</div>
	</div>
</template>

<script>
import axios from "axios";
export default {
	name: "App",
	methods: {
		passer_etape2: function() {
			// ajouter une condition de longueur du texte pour le prénom
			this.bloc1_prenom = false;
			this.bloc2_information = true;
		}
	},
	data: function() {
		return {
			prenom: "",
			bloc1_prenom: true,
			bloc2_information: false,
			jobSelected: "",
			jobList: ["Agile", "Data", "IT", "Autre"],
			coverimage:
				"https://images.unsplash.com/photo-1521737852567-6949f3f9f2b5?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1330&q=80",
			css: "https://cdnjs.cloudflare.com/ajax/libs/materialize/1.0.0/css/materialize.min.css",
			events: [
				{
					id: "257863509",
					link: "https://www.meetup.com/ParisAgileCommunity/events/257863509/",
					local_date: "2019-01-24",
					local_time: "19:00"
				},
				{
					id: "257530681",
					link: "https://www.meetup.com/Agile-Play-Ground/events/257530681/",
					local_date: "2019-02-19",
					local_time: "19:00"
				},
				{
					id: "257530702",
					link: "https://www.meetup.com/Agile-Play-Ground/events/257530702/",
					local_date: "2019-03-19",
					local_time: "19:00"
				},
				{
					id: "257530875",
					link: "https://www.meetup.com/Agile-Play-Ground/events/257530875/",
					local_date: "2019-04-16",
					local_time: "19:00"
				},
				{
					id: "258059231",
					link: "https://www.meetup.com/Agile-Play-Ground/events/258059231/",
					local_date: "2019-02-07",
					local_time: "19:00"
				},
				{
					id: "256339848",
					link: "https://www.meetup.com/ParisAgileCommunity/events/256339848/",
					local_date: "2019-01-22",
					local_time: "19:00"
				},
				{
					id: "257860695",
					link: "https://www.meetup.com/Agile-Nightmares-by-Digital-Catalysts/events/257860695/",
					local_date: "2019-01-17",
					local_time: "18:00"
				},
				{
					id: "257746440",
					link: "https://www.meetup.com/Agile-HR-Meetup/events/257746440/",
					local_date: "2019-01-23",
					local_time: "18:00"
				},
				{
					id: "257971516",
					link: "https://www.meetup.com/Meetup-Scrum-fr-Paris/events/257971516/",
					local_date: "2019-02-07",
					local_time: "19:00"
				},
				{
					id: "257448632",
					link:
						"https://www.meetup.com/Repetitions-Agile-France-Perfection-Games/events/257448632/",
					local_date: "2019-01-24",
					local_time: "18:30"
				},
				{
					id: "257587163",
					link: "https://www.meetup.com/dthinking-academy/events/257587163/",
					local_date: "2019-02-04",
					local_time: "13:00"
				},
				{
					id: "257587229",
					link: "https://www.meetup.com/dthinking-academy/events/257587229/",
					local_date: "2019-02-04",
					local_time: "14:00"
				},
				{
					id: "257866975",
					link: "https://www.meetup.com/We-Open-Space/events/257866975/",
					local_date: "2019-02-16",
					local_time: "09:30"
				},
				{
					id: "256121521",
					link: "https://www.meetup.com/dthinking-academy/events/256121521/",
					local_date: "2019-02-14",
					local_time: "09:00"
				},
				{
					id: "256125376",
					link: "https://www.meetup.com/dthinking-academy/events/256125376/",
					local_date: "2019-01-28",
					local_time: "10:00"
				},
				{
					id: "256596151",
					link: "https://www.meetup.com/dthinking-academy/events/256596151/",
					local_date: "2019-01-29",
					local_time: "09:00"
				},
				{
					id: "257588756",
					link: "https://www.meetup.com/dthinking-academy/events/257588756/",
					local_date: "2019-04-01",
					local_time: "09:00"
				},
				{
					id: "257588801",
					link: "https://www.meetup.com/dthinking-academy/events/257588801/",
					local_date: "2019-03-04",
					local_time: "09:00"
				},
				{
					id: "257588814",
					link: "https://www.meetup.com/dthinking-academy/events/257588814/",
					local_date: "2019-04-15",
					local_time: "09:00"
				},
				{
					id: "257588862",
					link: "https://www.meetup.com/dthinking-academy/events/257588862/",
					local_date: "2019-02-18",
					local_time: "10:00"
				}
			]
		};
	}
};
</script>

<style scoped>
.imagecover {
	width: 100%;
	height: 30vw;
	object-fit: cover;
	max-height: 450px;
	min-height: 120px;
}
.logo {
	object-fit: cover;
	width: 60%;
	height: 20vw;
	display: block;
	margin-left: auto;
	margin-right: auto;
}
label {
	font-size: 20px;
	margin-top: 35px;
	display: inline-block;
	color: #272728;
}
.fade-enter-active {
	transition: opacity 2s;
}
.fade-enter {
	opacity: 0;
}
#app {
}
</style>
