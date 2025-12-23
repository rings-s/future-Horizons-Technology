<script lang="ts">
	import './layout.css';
	import '$lib/i18n';
	import favicon from '$lib/assets/favicon.svg';
	import { locale, t } from 'svelte-i18n';
	import { page } from '$app/stores';

	let { children } = $props();

	// SEO metadata
	const siteName = 'Future Horizons Technology';
	const siteUrl = 'https://futurehorizonstechnology.pages.dev';
	const defaultImage = `${siteUrl}/og-image.png`;

	// Set lang and dir on the <html> element reactively
	$effect(() => {
		document.documentElement.lang = $locale || 'en';
		document.documentElement.dir = $locale === 'ar' ? 'rtl' : 'ltr';
	});
</script>

<svelte:head>
	<!-- Primary Meta Tags -->
	<title
		>{$t('seo.title') || 'Future Horizons Technology - Advanced Printing & Tech Solutions'}</title
	>
	<meta
		name="title"
		content={$t('seo.title') || 'Future Horizons Technology - Advanced Printing & Tech Solutions'}
	/>
	<meta
		name="description"
		content={$t('seo.description') ||
			'Future Horizons Technology provides cutting-edge printing solutions, managed print services, and innovative technology for businesses. Your trusted partner for digital transformation.'}
	/>
	<meta
		name="keywords"
		content="printing solutions, managed print services, technology, business solutions, Future Horizons, digital transformation, office equipment"
	/>
	<meta name="author" content="Future Horizons Technology" />
	<meta name="robots" content="index, follow" />
	<link rel="canonical" href={siteUrl + $page.url.pathname} />

	<!-- Favicon -->
	<link rel="icon" href={favicon} />
	<link rel="apple-touch-icon" href={favicon} />

	<!-- Preload LCP image -->
	<link rel="preload" as="image" href="/hero-device.png" fetchpriority="high" />

	<!-- Open Graph / Facebook -->
	<meta property="og:type" content="website" />
	<meta property="og:url" content={siteUrl + $page.url.pathname} />
	<meta
		property="og:title"
		content={$t('seo.title') || 'Future Horizons Technology - Advanced Printing & Tech Solutions'}
	/>
	<meta
		property="og:description"
		content={$t('seo.description') ||
			'Future Horizons Technology provides cutting-edge printing solutions, managed print services, and innovative technology for businesses.'}
	/>
	<meta property="og:image" content={defaultImage} />
	<meta property="og:site_name" content={siteName} />
	<meta property="og:locale" content={$locale === 'ar' ? 'ar_SA' : 'en_US'} />

	<!-- Twitter -->
	<meta property="twitter:card" content="summary_large_image" />
	<meta property="twitter:url" content={siteUrl + $page.url.pathname} />
	<meta
		property="twitter:title"
		content={$t('seo.title') || 'Future Horizons Technology - Advanced Printing & Tech Solutions'}
	/>
	<meta
		property="twitter:description"
		content={$t('seo.description') ||
			'Future Horizons Technology provides cutting-edge printing solutions, managed print services, and innovative technology for businesses.'}
	/>
	<meta property="twitter:image" content={defaultImage} />

	<!-- Theme Color -->
	<meta name="theme-color" content="#030712" />
</svelte:head>

{@render children()}
