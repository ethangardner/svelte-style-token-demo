<script lang="ts">
	interface Step {
		label: string;
		status: 'completed' | 'active' | 'default';
	}

	let { steps = [] }: { steps: readonly Step[] } = $props();
</script>

<div class="step-indicator">
	<ol class="steps">
		{#each steps as step}
			<li class="step" data-status={step.status}>
				<span class="marker"></span>
				<span class="label">{step.label}</span>
			</li>
		{/each}
	</ol>
</div>

<style>
	.step-indicator {
		/* Private internal aliases that map to public tokens or local defaults */
		--_color-default: var(--eg-c-step-indicator-color-default, var(--eg-s-color-neutral-100));
		--_color-active: var(--eg-c-step-indicator-color-active, var(--eg-s-color-cool-100));
		--_color-completed: var(--eg-c-step-indicator-color-completed, var(--eg-s-color-warm-100));

		--_marker-size: var(--eg-c-step-indicator-item-marker-size, var(--eg-s-size-8, 0.5rem));
		--eg-c-step-indicator-steps-gap: var(--eg-t-spacing-md);
		--eg-c-step-indicator-step-gap: var(--eg-t-spacing-xxs, var(--eg-s-size-4, 0.25rem));
		font-family: var(--eg-t-font-family-sans);
	}

	.steps {
		display: flex;
		list-style: none;
		padding: 0;
		gap: var(--eg-c-step-indicator-steps-gap);
	}

	.step {
		display: flex;
		flex-direction: column;
		align-items: center;
		gap: var(--eg-c-step-indicator-step-gap);
		flex: 1;
		position: relative;
	}

	/* Connector line */
	.step:not(:last-child)::after {
		content: '';
		position: absolute;
		top: calc(var(--_marker-size) / 2);
		left: calc(50% + var(--_marker-size) / 2);
		width: calc(100% - var(--_marker-size));
		height: 2px;
		background-color: var(--_color-default);
		z-index: 0;
	}

	.step[data-status='completed']:not(:last-child)::after {
		background-color: var(--_color-completed);
	}

	.marker {
		width: var(--_marker-size);
		height: var(--_marker-size);
		border-radius: 50%;
		background-color: var(--_color-default);
		border: 2px solid var(--_color-default);
		z-index: 1;
	}

	.label {
		font-size: var(--eg-t-font-size-sm, 0.875rem);
		color: var(--_color-default);
		text-align: center;
	}

	.step[data-status='active'] .marker {
		background-color: var(--_color-active);
		border-color: var(--_color-active);
		outline: 2px solid var(--_color-active);
		outline-offset: 2px;
	}

	.step[data-status='active'] .label {
		color: var(--_color-active);
		font-weight: bold;
	}

	.step[data-status='completed'] .marker {
		background-color: var(--_color-completed);
		border-color: var(--_color-completed);
	}

	.step[data-status='completed'] .label {
		color: var(--_color-completed);
	}
</style>
