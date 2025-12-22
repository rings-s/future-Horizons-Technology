<script lang="ts">
	import './layout.css';
	import favicon from '$lib/assets/favicon.svg';
	import { locale } from 'svelte-i18n';
	
	let { children } = $props();
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
	<html lang={$locale || 'en'} dir={$locale === 'ar' ? 'rtl' : 'ltr'} />
</svelte:head>

{@render children()}
