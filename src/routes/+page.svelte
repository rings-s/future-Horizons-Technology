<script lang="ts">
	import './layout.css';
	import '$lib/i18n';
	import { locale, isLoading } from 'svelte-i18n';
	import Header from '$lib/components/header.svelte';
	import HeroSection from '$lib/components/hero-section.svelte';
	import MarqueeSection from '$lib/components/marquee-section.svelte';
	import FeaturesSection from '$lib/components/features-section.svelte';
	import StatsSection from '$lib/components/stats-section.svelte';
	import AboutSection from '$lib/components/about-section.svelte';
	import ServicesSection from '$lib/components/services-section.svelte';
	import ProductsSection from '$lib/components/products-section.svelte';
	import ValuesSection from '$lib/components/values-section.svelte';
	import ClientsSection from '$lib/components/clients-section.svelte';
	import ContactSection from '$lib/components/contact-section.svelte';
	import Footer from '$lib/components/footer.svelte';

	// Update dir attribute based on locale
	$: if (typeof document !== 'undefined') {
		document.documentElement.dir = $locale === 'ar' ? 'rtl' : 'ltr';
		document.documentElement.lang = $locale || 'en';
	}
</script>

{#if $isLoading}
	<div class="min-h-screen bg-background flex items-center justify-center">
		<div class="flex flex-col items-center gap-4">
			<div
				class="w-12 h-12 border-4 border-primary border-t-transparent rounded-full animate-spin"
			></div>
			<p class="text-muted-foreground">Loading...</p>
		</div>
	</div>
{:else}
	<main class="min-h-screen bg-background">
		<Header />
		<HeroSection />
		<MarqueeSection />
		<FeaturesSection />
		<StatsSection />
		<AboutSection />
		<ServicesSection />
		<ProductsSection />
		<ValuesSection />
		<ClientsSection />
		<ContactSection />
		<Footer />
	</main>
{/if}
