<script lang="ts">
	import './layout.css';
	import '$lib/i18n';
	import { locale } from 'svelte-i18n';
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
