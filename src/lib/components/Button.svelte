<script lang="ts">
	import type { Snippet } from 'svelte';

	interface Props {
		children: Snippet;
		type?: 'button' | 'submit' | 'reset';
		variant?: 'primary' | 'secondary' | 'outline';
		onclick?: (e: MouseEvent) => void;
	}

	let { 
		children, 
		type = 'button', 
		variant = 'primary',
		onclick 
	}: Props = $props();
</script>

<button {type} class="btn" data-variant={variant} {onclick}>
	{@render children()}
</button>

<style>
	.btn {
		/* Private internal aliases mapped to public component tokens or defaults */
		--_bg: var(--eg-c-button-bg, var(--eg-t-body-color, #000));
		--_fg: var(--eg-c-button-fg, var(--eg-t-body-background, #fff));
		--_padding: var(--eg-c-button-padding, var(--eg-t-spacing-md, 1rem));
		--_radius: var(--eg-c-button-radius, var(--eg-s-size-4, 0.25rem));
		--_border: var(--eg-c-button-border, 1px solid transparent);

		/* Hover adjustment factor: negative to darken in light mode, positive to lighten in dark mode */
		--_l-offset: -0.1;

		display: inline-flex;
		align-items: center;
		justify-content: center;
		padding: calc(var(--_padding) / 2) var(--_padding);
		background-color: var(--_bg);
		color: var(--_fg);
		border: var(--_border);
		border-radius: var(--_radius);
		font-family: var(--eg-t-font-family-sans);
		font-size: var(--eg-t-font-size-md);
		cursor: pointer;
		transition: background-color 0.2s, color 0.2s, border-color 0.2s;
	}

	@media (prefers-color-scheme: dark) {
		.btn {
			--_l-offset: 0.1;
		}
	}

	.btn:hover {
		background-color: oklch(from var(--_bg) calc(l + var(--_l-offset)) c h);
	}

	.btn[data-variant='secondary'] {
		--_bg: var(--eg-c-button-secondary-bg, var(--eg-s-color-neutral-40));
		--_fg: var(--eg-c-button-secondary-fg, var(--eg-s-color-neutral-210));
	}

	.btn[data-variant='outline'] {
		--_bg: transparent;
		--_fg: var(--eg-c-button-outline-fg, var(--eg-t-body-color));
		--_border: 1px solid var(--_fg);
	}

	.btn[data-variant='outline']:hover {
		--_hover-fg: oklch(from var(--_fg) calc(l + var(--_l-offset)) c h);
		background-color: transparent;
		color: var(--_hover-fg);
		border-color: var(--_hover-fg);
	}
</style>
