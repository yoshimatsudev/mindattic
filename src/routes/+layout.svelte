<script lang="ts">
	import '../app.postcss';
	import { AppShell } from '@skeletonlabs/skeleton';
	import { AppBar } from '@skeletonlabs/skeleton';
	import { LightSwitch } from '@skeletonlabs/skeleton';
	import { PlaySquare, Headphones, Volume, Volume1, Volume2 } from 'lucide-svelte';
	import { RangeSlider } from '@skeletonlabs/skeleton';
	let volume = 10;
	let openVolumeContext = false;
	let muteState = false;

	$: volumelog = volume;

	console.log(volumelog)
</script>

<AppShell slotPageFooter="mb-10">
	<svelte:fragment slot="header">Header</svelte:fragment>
	<svelte:fragment slot="sidebarLeft">Sidebar Left</svelte:fragment>
	<svelte:fragment slot="sidebarRight">Sidebar Right</svelte:fragment>
	<svelte:fragment slot="pageHeader">Page Header</svelte:fragment>
	<!-- Router Slot -->
	<slot />
	<!-- ---- / ---- -->
	<svelte:fragment slot="pageFooter">
		<AppBar
			border="rounded-full"
			shadow="shadow-md"
			background="bg-secondary-300 dark:bg-secondary-900"
			gridColumns="grid-cols-3"
			slotDefault=""
			slotTrail="place-content-end"
		>
			<svelte:fragment slot="lead"><LightSwitch /></svelte:fragment>
			<section class="flex justify-around">
				<button class="btn btn-icon"><PlaySquare /></button>
				<button
					class={!muteState
						? 'bg-secondary-300 dark:bg-secondary-900 btn btn-icon'
						: 'bg-error-600 btn btn-icon'}
					on:click={() => {
						muteState = !muteState;
					}}><Headphones /></button
				>
				<div class="flex items-center">
					<button class={'bg-secondary-300 dark:bg-secondary-900 btn btn-icon'} on:click={() => {
						openVolumeContext = !openVolumeContext;
					}}>
					{#if volume == 0}
					<Headphones/>
					{:else if volume <= 50}
					<Volume/>
					{:else if volume >= 50}
					<Volume1/>
					{:else if volume >= 60}
					<Volume2/>
					{/if}
					</button>
					<RangeSlider name="range-slider" bind:value={volume} on:change={() => console.log(volume)} max={100} class={openVolumeContext ? "" : "hidden"} />
				</div>
			</section>
			<svelte:fragment slot="trail">teste</svelte:fragment>
		</AppBar>
	</svelte:fragment>
	<svelte:fragment slot="footer" />
</AppShell>
