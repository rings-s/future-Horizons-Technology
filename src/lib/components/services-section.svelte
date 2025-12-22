<script>
	import { onMount } from 'svelte';
	import {
		ShoppingCart,
		Package,
		Wrench,
		Settings,
		LineChart,
		Headphones,
		ArrowRight
	} from 'lucide-svelte';
	import { t } from 'svelte-i18n';

	const services = [
		{
			icon: ShoppingCart,
			titleKey: 'services.salesRental.title',
			descriptionKey: 'services.salesRental.description'
		},
		{
			icon: Package,
			titleKey: 'services.supplies.title',
			descriptionKey: 'services.supplies.description'
		},
		{
			icon: Wrench,
			titleKey: 'services.maintenance.title',
			descriptionKey: 'services.maintenance.description'
		},
		{
			icon: Settings,
			titleKey: 'services.installation.title',
			descriptionKey: 'services.installation.description'
		},
		{
			icon: LineChart,
			titleKey: 'services.printManagement.title',
			descriptionKey: 'services.printManagement.description'
		},
		{
			icon: Headphones,
			titleKey: 'services.ongoingSupport.title',
			descriptionKey: 'services.ongoingSupport.description'
		}
	];

	let isVisible = $state(false);
	let sectionRef;

	onMount(() => {
		const observer = new IntersectionObserver(
			([entry]) => {
				if (entry.isIntersecting) {
					isVisible = true;
				}
			},
			{ threshold: 0.1 }
		);

		if (sectionRef) {
			observer.observe(sectionRef);
		}

		return () => observer.disconnect();
	});
</script>

<section
	bind:this={sectionRef}
	id="services"
	class="relative py-24 lg:py-32 bg-gradient-to-b from-background via-secondary/10 to-background overflow-hidden"
>
	<div class="container mx-auto px-4 sm:px-6 lg:px-8 relative z-10">
		<!-- Header -->
		<div class="text-center max-w-3xl mx-auto mb-20">
			<div
				class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-primary/10 text-primary text-sm font-medium mb-6 transition-all duration-700 {isVisible
					? 'opacity-100 translate-y-0'
					: 'opacity-0 translate-y-4'}"
			>
				{$t('services.badge')}
			</div>
			<h2
				class="text-4xl sm:text-5xl font-bold text-foreground mb-6 transition-all duration-700 delay-100 {isVisible
					? 'opacity-100 translate-y-0'
					: 'opacity-0 translate-y-8'}"
			>
				{$t('services.title')}
				<span class="text-transparent bg-clip-text bg-gradient-to-r from-primary to-blue-500"
					>{$t('services.titleHighlight')}</span
				>
			</h2>
			<p
				class="text-xl text-muted-foreground leading-relaxed transition-all duration-700 delay-200 {isVisible
					? 'opacity-100 translate-y-0'
					: 'opacity-0 translate-y-8'}"
			>
				{$t('services.subtitle')}
			</p>
		</div>

		<!-- Services Grid -->
		<div class="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
			{#each services as service, index}
				<div
					class="group p-8 rounded-3xl glass border border-white/5 hover:border-primary/20 hover:bg-white/5 transition-all duration-500 hover:-translate-y-2 {isVisible
						? 'opacity-100 translate-y-0'
						: 'opacity-0 translate-y-12'}"
					style="transition-delay: {index * 100}ms"
				>
					<div
						class="w-14 h-14 rounded-2xl bg-primary/10 flex items-center justify-center mb-6 group-hover:scale-110 group-hover:bg-primary group-hover:text-white transition-all duration-500"
					>
						<svelte:component this={service.icon} class="w-7 h-7 transition-colors" />
					</div>
					<h3
						class="text-xl font-bold text-foreground mb-3 group-hover:text-primary transition-colors"
					>
						{$t(service.titleKey)}
					</h3>
					<p class="text-muted-foreground leading-relaxed mb-6">{$t(service.descriptionKey)}</p>
					<a
						href="#contact"
						class="inline-flex items-center gap-2 text-sm font-medium text-primary hover:gap-3 transition-all"
					>
						{$t('services.learnMore')}
						<ArrowRight class="w-4 h-4" />
					</a>
				</div>
			{/each}
		</div>
	</div>
</section>
