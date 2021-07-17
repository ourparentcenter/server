<!--
	- @copyright 2021, Christopher Ng <chrng8@gmail.com>
	-
	- @author Christopher Ng <chrng8@gmail.com>
	-
	- @license GNU AGPL version 3 or any later version
	-
	- This program is free software: you can redistribute it and/or modify
	- it under the terms of the GNU Affero General Public License as
	- published by the Free Software Foundation, either version 3 of the
	- License, or (at your option) any later version.
	-
	- This program is distributed in the hope that it will be useful,
	- but WITHOUT ANY WARRANTY; without even the implied warranty of
	- MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
	- GNU Affero General Public License for more details.
	-
	- You should have received a copy of the GNU Affero General Public License
	- along with this program. If not, see <http://www.gnu.org/licenses/>.
-->

<template>
	<h3>
		<label :for="labelFor">
			{{ t('settings', title) }}
		</label>

		<FederationControl class="federation-control"
			:account-property="accountProperty"
			:handle-scope-change="handleScopeChange"
			:scope.sync="localScope"
			@update:scope="onScopeChange" />

		<AddButton v-if="isEditable && isMultiValueSupported"
			class="add-button"
			:disabled="!isValidForm"
			@click.stop.prevent="onAddAdditional" />
	</h3>
</template>

<script>
import FederationControl from './FederationControl'
import AddButton from './AddButton'

export default {
	name: 'HeaderBar',

	components: {
		FederationControl,
		AddButton,
	},

	props: {
		title: {
			type: String,
			required: true,
		},
		labelFor: {
			type: String,
			required: true,
		},
		isEditable: {
			type: Boolean,
			required: true,
		},
		isMultiValueSupported: {
			type: Boolean,
			default: false,
		},
		isValidForm: {
			type: Boolean,
			default: true,
		},
		scope: {
			type: String,
			required: true,
		},
		handleScopeChange: {
			type: Function,
			required: true,
		},
	},

	data() {
		return {
			accountProperty: this.title.toLowerCase(),
			localScope: this.scope,
		}
	},

	methods: {
		onAddAdditional() {
			this.$emit('addAdditional')
		},

		onScopeChange(scope) {
			this.$emit('update:scope', scope)
		},
	},
}
</script>

<style lang="scss" scoped>
	.federation-control {
		margin: -12px 0 0 8px;
	}

	.add-button {
		margin: -12px 0 0 auto !important;
	}
</style>
