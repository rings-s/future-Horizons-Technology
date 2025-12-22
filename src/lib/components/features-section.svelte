<script lang="ts">
	import { onMount } from 'svelte';
	import { Printer, Wrench, Package, Headphones, Shield, Zap, ArrowUpRight } from 'lucide-svelte';
	import { t } from 'svelte-i18n';

	const features = [
		{
			icon: Printer,
			titleKey: 'features.salesRental.title',
			descriptionKey: 'features.salesRental.description',
			color: 'from-cyan-500/20 to-teal-500/20',
			borderColor: 'border-cyan-500/30',
			iconColor: 'text-cyan-400'
		},
		{
			icon: Wrench,
			titleKey: 'features.maintenance.title',
			descriptionKey: 'features.maintenance.description',
			color: 'from-emerald-500/20 to-green-500/20',
			borderColor: 'border-emerald-500/30',
			iconColor: 'text-emerald-400'
		},
		{
			icon: Package,
			titleKey: 'features.parts.title',
			descriptionKey: 'features.parts.description',
			color: 'from-blue-500/20 to-indigo-500/20',
			borderColor: 'border-blue-500/30',
			iconColor: 'text-blue-400'
		},
		{
			icon: Headphones,
			titleKey: 'features.support247.title',
			descriptionKey: 'features.support247.description',
			color: 'from-purple-500/20 to-violet-500/20',
			borderColor: 'border-purple-500/30',
			iconColor: 'text-purple-400'
		},
		{
			icon: Shield,
			titleKey: 'features.contracts.title',
			descriptionKey: 'features.contracts.description',
			color: 'from-amber-500/20 to-orange-500/20',
			borderColor: 'border-amber-500/30',
			iconColor: 'text-amber-400'
		},
		{
			icon: Zap,
			titleKey: 'features.solutions.title',
			descriptionKey: 'features.solutions.description',
			color: 'from-rose-500/20 to-pink-500/20',
			borderColor: 'border-rose-500/30',
			iconColor: 'text-rose-400'
		}
	];

	let isVisible = $state(false);
	let sectionRef: HTMLElement;

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

<section bind:this={sectionRef} id="features" class="relative py-32 overflow-hidden bg-background">
	<!-- Background elements -->
	<div
		class="absolute inset-0 bg-[radial-gradient(circle_at_top_right,rgba(var(--primary-rgb),0.05),transparent_40%)]"
	></div>
	<div
		class="absolute inset-0 bg-[radial-gradient(circle_at_bottom_left,rgba(59,130,246,0.05),transparent_40%)]"
	></div>

	<div class="container mx-auto px-4 sm:px-6 lg:px-8 relative z-10">
		<!-- Section header -->
		<div class="text-center mb-20">
			<div
				class="inline-flex items-center gap-2 px-4 py-2 rounded-full glass border border-primary/10 mb-8 transition-all duration-700 {isVisible
					? 'opacity-100 translate-y-0'
					: 'opacity-0 translate-y-4'}"
			>
				<span class="relative flex h-2 w-2">
					<span
						class="animate-ping absolute inline-flex h-full w-full rounded-full bg-primary opacity-75"
					></span>
					<span class="relative inline-flex rounded-full h-2 w-2 bg-primary"></span>
				</span>
				<span class="text-sm text-primary font-medium tracking-wide">{$t('features.badge')}</span>
			</div>

			<h2
				class="text-4xl sm:text-5xl lg:text-6xl font-bold text-foreground mb-6 text-balance tracking-tight transition-all duration-700 delay-100 {isVisible
					? 'opacity-100 translate-y-0'
					: 'opacity-0 translate-y-8'}"
			>
				{$t('features.title')}
				<span class="text-transparent bg-clip-text bg-gradient-to-r from-primary to-blue-500"
					>{$t('features.titleHighlight')}</span
				>
			</h2>

			<p
				class="text-xl text-muted-foreground max-w-2xl mx-auto leading-relaxed transition-all duration-700 delay-200 {isVisible
					? 'opacity-100 translate-y-0'
					: 'opacity-0 translate-y-8'}"
			>
				{$t('features.subtitle')}
			</p>
		</div>

		<!-- Features grid -->
		<div class="grid md:grid-cols-2 lg:grid-cols-3 gap-6 lg:gap-8">
			{#each features as feature, index}
				{@const Icon = feature.icon}
				<div
					class="group relative p-8 rounded-3xl glass border border-white/5 hover:border-white/10 transition-all duration-500 hover:-translate-y-2 {isVisible
						? 'opacity-100 translate-y-0'
						: 'opacity-0 translate-y-8'}"
					style="transition-delay: {index * 100}ms"
				>
					<!-- Hover Gradient -->
					<div
						class="absolute inset-0 bg-gradient-to-br {feature.color} opacity-0 group-hover:opacity-100 transition-opacity duration-500 rounded-3xl"
					></div>

					<!-- Content -->
					<div class="relative z-10">
						<div class="flex items-start justify-between mb-6">
							<div
								class="w-14 h-14 rounded-2xl bg-background/50 backdrop-blur-md border border-white/10 flex items-center justify-center group-hover:scale-110 transition-transform duration-500 shadow-lg"
							>
								<Icon class="w-7 h-7 {feature.iconColor}" />
							</div>
							<div
								class="w-8 h-8 rounded-full bg-white/5 flex items-center justify-center opacity-0 group-hover:opacity-100 -translate-x-2 group-hover:translate-x-0 transition-all duration-300"
							>
								<ArrowUpRight class="w-4 h-4 text-white" />
							</div>
						</div>

						<h3
							class="text-xl font-bold text-foreground mb-3 group-hover:text-primary transition-colors"
						>
							{$t(feature.titleKey)}
						</h3>
						<p
							class="text-muted-foreground/80 leading-relaxed text-sm group-hover:text-muted-foreground transition-colors"
						>
							{$t(feature.descriptionKey)}
						</p>
					</div>
				</div>
			{/each}
		</div>

		<!-- Bottom CTA -->
		<div
			class="mt-20 text-center transition-all duration-700 delay-500 {isVisible
				? 'opacity-100 translate-y-0'
				: 'opacity-0 translate-y-8'}"
		>
			<div class="inline-flex flex-col items-center gap-4">
				<p class="text-muted-foreground mb-3">{$t('features.cta')}</p>
				<a
					href="#contact"
					class="text-primary font-medium hover:underline inline-flex items-center gap-2 group"
				>
					{$t('features.ctaLink')}
					<ArrowUpRight
						class="w-4 h-4 group-hover:translate-x-0.5 group-hover:-translate-y-0.5 transition-transform"
					/>
				</a>
			</div>
		</div>
	</div>
</section>
