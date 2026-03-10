<script lang="ts">
	import StepIndicator from '$lib/components/StepIndicator.svelte';
	import Button from '$lib/components/Button.svelte';

	const steps = [
		{ label: 'Step 1', status: 'completed' },
		{ label: 'Step 2', status: 'completed' },
		{ label: 'Step 3', status: 'completed' },
		{ label: 'Step 4', status: 'active' },
		{ label: 'Step 5', status: 'default' }
	] as const;
</script>

<svelte:head>
	<title>Style Token Adaptation</title>
</svelte:head>

<main>
	<h1>Style Token Adaptation</h1>
	<p>Adapting Ethan Gardner's Web Component style token approach to Svelte 5.</p>

	<section>
		<h2>Step Indicator (Default Theme)</h2>
		<StepIndicator {steps} />
	</section>

	<section class="custom-theme">
		<h2>Step Indicator (Custom Local Theme)</h2>
		<p>Using <code>--eg-c-step-indicator-color-active: hotpink;</code> via local scope.</p>
		<StepIndicator {steps} />
	</section>

	<section>
		<h2>Button Components</h2>
		<div class="button-group">
			<Button>Primary Button</Button>
			<Button variant="secondary">Secondary Button</Button>
			<Button variant="outline">Outline Button</Button>
		</div>
	</section>

	<section class="custom-buttons">
		<h2>Themed Buttons</h2>
		<p>Overriding button tokens locally.</p>
		<div class="button-group">
			<Button>Custom Primary</Button>
			<Button variant="outline">Custom Outline</Button>
		</div>
	</section>
</main>

<style>
	main {
		display: flex;
		flex-direction: column;
		gap: var(--eg-t-spacing-lg);
		max-width: 800px;
	}

	section {
		display: flex;
		flex-direction: column;
		gap: var(--eg-t-spacing-md);
		padding: var(--eg-t-spacing-md);
		border: 1px solid var(--eg-s-color-neutral-40);
		border-radius: 8px;
	}

	.button-group {
		display: flex;
		gap: var(--eg-t-spacing-md);
		flex-wrap: wrap;
	}

	.custom-theme {
		/* Locally overriding component tokens */
		--eg-c-step-indicator-color-active: hotpink;
		--eg-c-step-indicator-item-marker-size: 14px;
	}

	.custom-buttons {
		/* Locally overriding component tokens for Button */
		--eg-c-button-bg: var(--eg-s-color-warm-120);
		--eg-c-button-fg: var(--eg-s-color-warm-10);
		--eg-c-button-radius: var(--eg-s-size-20);
		--eg-c-button-outline-fg: var(--eg-s-color-warm-140);
	}

	@media (prefers-color-scheme: dark) {
		.custom-buttons {
			--eg-c-button-outline-fg: var(--eg-s-color-cool-30);
		}
	}
</style>
