<script lang="ts">
	import { type, version } from '@tauri-apps/plugin-os';

	async function getData() {
		try {
			const osType = await type();
			const osVersion = await version();
			return {
				osType,
				osVersion
			};
		} catch (error) {
			return {
				osType: 'web',
				osVersion: '1.0.0'
			};
		}
	}
</script>

<svelte:head>
	{#await getData() then { osType }}
		{#if osType !== 'web'}
			<meta name="viewport" content="width=device-width, user-scalable=no" />
		{/if}
	{/await}
</svelte:head>

<main>
	<slot></slot>
</main>

<style lang="scss">
	:global(body) {
		--background-color: hsl(184, 30%, 90%);
		--primary-500: hsl(184, 30%, 60%);
		--text-500: hsl(184, 30%, 20%);
		--text-700: hsl(184, 30%, 10%);

		--size-large: 1.5rem;
		--size-default: 1rem;
		--size-small: 0.75rem;
		--size-border-radius: 0.25rem;

		--font-family-default: 'Futura, sans-serif';
		--font-family-heading: 'Verdana';

		box-sizing: border-box;
		background-color: var(--background-color);
		font-family: Verdana, Geneva, Tahoma, sans-serif;
		color: var(--text-500);
		margin: 0;
		padding: 0;
	}

	main {
		display: flex;
		flex-direction: column;
		padding: 0 1rem;
		max-width: 16rem;
		gap: var(--size-default);
		margin: 0 auto;
	}

	:global(h1) {
		font-family: var(--font-family-heading);
		color: var(--text-700);
		font-size: var(--size-large);
		padding: 0;
		margin: 0;
	}

	:global(p) {
		font-size: var(--size-default);
		padding: 0;
		margin: 0;
	}

	:global(button) {
		user-select: none;
		-webkit-user-select: none;
		height: var(--size-large);
		font-size: var(--size-default);
	}
</style>
