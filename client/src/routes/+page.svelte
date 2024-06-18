<script lang="ts">
	import { type, version } from '@tauri-apps/plugin-os';
	let count = $state(0);

	async function getData() {
		try {
			const osType = await type();
			const osVersion = await version();
			return {
				osType,
				osVersion
			};
		} catch (error) {
			throw new Error('Something went wrong.');
		}
	}
</script>

<h1>Svauri</h1>
<p>Welcome to Svauri, the most incredible app on planet earth.</p>
<button onclick={() => (count += 1)}>Increment counter</button>

<div class="card">
	<span class="value">{count}</span>
	<span class="label">Counter</span>
</div>

<p>
	<a href="./about">Go to aboot page</a>
</p>

<p>
	{#await getData()}
		Loading platform data...
	{:then data}
		Current os: {data.osType}
		{data.osVersion}
		{#if data.osType === 'macos'}
			🍏
		{:else if data.osType === 'windows'}
			🪟
		{:else if data.osType === 'linux'}
			🐧
		{:else if data.osType === 'android'}
			🤖
		{:else if data.osType === 'ios'}
			📱
		{:else}
			🤷‍♂️
		{/if}
	{:catch error}
		Error: {error.message}
	{/await}
</p>

<style lang="scss">
	.card {
		display: flex;
		flex-direction: column;
		align-items: center;

		background-color: var(--background-color);
		border-radius: var(--size-border-radius);
		border: 1px solid var(--primary-500);
		padding: var(--size-default);
	}

	.value {
		font-size: var(--size-large);
	}

	.label {
		font-size: var(--size-small);
	}
</style>
