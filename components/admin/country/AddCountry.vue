<template>
	<modal @close="$emit('close')">
		<h3>{{ isEdit ? 'Edit country' : 'Create country' }}</h3>
		<validation-observer v-slot="{ handleSubmit }">
			<form class="forms-sample" @submit.prevent="handleSubmit(onSubmit)">
				<div class="form-group">
					<label for="title">Name</label>
					<validation-provider v-slot="{ errors }" rules="required">
						<input id="title" v-model="country.name" :class="{ 'is-invalid' : errors.length }" type="text" class="form-control" placeholder="Name">
						<span class="invalid-feedback">{{ errors[0] }}</span>
					</validation-provider>
				</div>
				<div class="form-group">
					<label for="iso-code">ISO Code</label>
					<validation-provider v-slot="{ errors }" rules="required">
						<input id="iso-code" v-model="country.iso_code" type="text" :class="{ 'is-invalid' : errors.length }" class="form-control" placeholder="ISO Code">
						<span class="invalid-feedback">{{ errors[0] }}</span>
					</validation-provider>
				</div>
				<button type="submit" class="btn btn-primary mr-2">Submit</button>
				<button class="btn btn-light" @click.prevent="$emit('close')">Cancel</button>
			</form>
		</validation-observer>
	</modal>
</template>

<script>
import Modal from '@/components/common/Modal.vue'
import { ValidationObserver, ValidationProvider } from 'vee-validate'
import { countryService } from '@/_services/country.service'

export default {
	name: 'AddCountry',
	components: { Modal, ValidationProvider, ValidationObserver },
	props: {
		isEdit: { type: Boolean, default: false },
		currentCountry: { type: Object, default: () => ({}) }
	},
	data () {
		return {
			country: {}
		}
	},
	mounted () {
		if (this.isEdit) {
			this.country = this.currentCountry
		}
	},
	methods: {
		onSubmit () {
			if (this.isEdit) {
				countryService.edit(this.country, this.country.id).then(() => {
					this.$toast.success('Successfully updated')
					this.$emit('close')
					this.$emit('fetch')
				}).catch(err => {
					this.$toast.error(err)
				})
			} else {
				countryService.create(this.country).then(() => {
					this.$toast.success('Successfully created')
					this.$emit('close')
					this.$emit('fetch')
				}).catch(err => {
					this.$toast.error(err)
				})
			}
		}
	}
}
</script>

<style>

</style>