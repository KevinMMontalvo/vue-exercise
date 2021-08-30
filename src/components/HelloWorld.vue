<template>
	<v-container>
		<v-form ref="form">
			<v-row class="text-center">
				<v-col cols="6">
					<!--Textfield del nombre-->
				</v-col>
				<v-col cols="6">
					<!--Textfield del apellido-->
				</v-col>
				<v-col cols="12">
					<!--Boton-->
				</v-col>
			</v-row>
			<v-snackbar v-model="message.visible" :color="message.color">{{ message.text }}</v-snackbar>
		</v-form>
	</v-container>
</template>

<script>
import axios from "axios";

export default {
	name: 'HelloWorld',

	data: () => ({
		name: '',
		surname: '',
		message: {
			visible: false,
			color: '',
			text: ''
		}
	}),
	methods: {
		save()
		{
			let data = this.$data;

			let item = {
				username: this.name,
				email: this.surname,
				password: 'pass'
			};

			axios.post('https://autorepuestos-dev.herokuapp.com/signup', item).then(function (response)
			{
				data.message = {
					visible: true,
					text: 'Usuario creado',
					color: 'success'
				};
				data.name = '';
				data.surname = '';
			}).catch(function (error)
			{
				console.error(error);
				data.message = {
					visible: true,
					text: 'Hubo un error al crear el usuario',
					color: 'error'
				};
			}).then(function ()
			{
			});
		}
	}
};
</script>
