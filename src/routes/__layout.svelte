<script lang="ts">
	import type { TopAppBarComponentDev } from '@smui/top-app-bar';
	import TopAppBar, { Row, Section, Title, AutoAdjust } from '@smui/top-app-bar';
	import IconButton, { Icon } from '@smui/icon-button';
	import { mdiMenu, mdiWeatherSunny, mdiWeatherNight } from '@mdi/js';
	import { Svg } from '@smui/common/elements';
	import { onMount } from 'svelte';
	let topAppBar: TopAppBarComponentDev;

	let darkTheme: boolean | undefined = undefined;

	onMount(() => {
		darkTheme = window.matchMedia('(prefers-color-scheme: dark)').matches;
	});
</script>

<svelte:head>
	<!-- SMUI Styles -->
	{#if darkTheme === undefined}
		<link rel="stylesheet" href="/smui.css" media="(prefers-color-scheme: light)" />
		<link rel="stylesheet" href="/smui-dark.css" media="screen and (prefers-color-scheme: dark)" />
	{:else if darkTheme}
		<link rel="stylesheet" href="/smui.css" />
		<link rel="stylesheet" href="/smui-dark.css" media="screen" />
	{:else}
		<link rel="stylesheet" href="/smui.css" />
	{/if}
</svelte:head>
<TopAppBar bind:this={topAppBar} variant="standard">
	<Row>
		<Section>
			<IconButton>
				<Icon component={Svg} viewBox="0 0 24 24">
					<path fill="currentColor" d={mdiMenu} />
				</Icon></IconButton
			>
			<Title>Standard</Title>
		</Section>
		<Section align="end" toolbar>
			<IconButton
				on:click={() => {
					darkTheme = !darkTheme;
				}}
				title={darkTheme ? 'Switch to light theme' : 'Switch to dark theme'}
			>
				<Icon component={Svg} viewBox="0 0 24 24">
					<path fill="currentColor" d={darkTheme ? mdiWeatherSunny : mdiWeatherNight} />
				</Icon></IconButton
			>
		</Section>
	</Row>
</TopAppBar>
<AutoAdjust {topAppBar}>
	<slot />
</AutoAdjust>
