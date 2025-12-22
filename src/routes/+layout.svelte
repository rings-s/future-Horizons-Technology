<script lang="ts">
	import './layout.css';
	import favicon from '$lib/assets/favicon.svg';
	import { locale } from 'svelte-i18n';

	let { children } = $props();

	// Set lang and dir on the <html> element reactively
	$effect(() => {
		document.documentElement.lang = $locale || 'en';
		document.documentElement.dir = $locale === 'ar' ? 'rtl' : 'ltr';
	});
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
</svelte:head>

{@render children()}
