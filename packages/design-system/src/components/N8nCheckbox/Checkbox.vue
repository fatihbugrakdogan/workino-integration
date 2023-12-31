<template>
	<el-checkbox
		v-bind="$props"
		ref="checkbox"
		:class="['n8n-checkbox', $style.n8nCheckbox]"
		:disabled="disabled"
		:indeterminate="indeterminate"
		:modelValue="modelValue"
		@update:modelValue="onUpdateModelValue"
	>
		<slot></slot>
		<n8n-input-label
			v-if="label"
			:label="label"
			:tooltipText="tooltipText"
			:bold="false"
			:size="labelSize"
			@click.prevent="onLabelClick"
		/>
	</el-checkbox>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import { ElCheckbox } from 'element-plus';
import N8nInputLabel from '../N8nInputLabel';

export default defineComponent({
	name: 'n8n-checkbox',
	components: {
		ElCheckbox,
		N8nInputLabel,
	},
	props: {
		label: {
			type: String,
		},
		disabled: {
			type: Boolean,
			default: false,
		},
		tooltipText: {
			type: String,
		},
		indeterminate: {
			type: Boolean,
			default: false,
		},
		modelValue: {
			type: Boolean,
			default: false,
		},
		labelSize: {
			type: String,
			default: 'medium',
			validator: (value: string): boolean => ['small', 'medium'].includes(value),
		},
	},
	methods: {
		onUpdateModelValue(value: boolean) {
			this.$emit('update:modelValue', value);
		},
		onLabelClick() {
			const checkboxComponent = this.$refs.checkbox as ElCheckbox;
			if (!checkboxComponent) {
				return;
			}

			(checkboxComponent.$el as HTMLElement).click();
		},
	},
});
</script>

<style lang="scss" module>
.n8nCheckbox {
	display: flex !important;
	white-space: normal !important;
	margin-bottom: var(--spacing-2xs);

	span {
		white-space: normal;
	}

	label {
		cursor: pointer;
		margin-bottom: 0;
	}
}
</style>
