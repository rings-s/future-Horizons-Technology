<script>
	import { onMount } from 'svelte';
	import { Lightbulb, Shield, Users, Clock, Award } from 'lucide-svelte';
	import { t } from 'svelte-i18n';

	const values = [
		{
			icon: Lightbulb,
			titleKey: 'values.innovation.title',
			descriptionKey: 'values.innovation.description'
		},
		{ icon: Award, titleKey: 'values.quality.title', descriptionKey: 'values.quality.description' },
		{
			icon: Shield,
			titleKey: 'values.transparency.title',
			descriptionKey: 'values.transparency.description'
		},
		{
			icon: Clock,
			titleKey: 'values.commitment.title',
			descriptionKey: 'values.commitment.description'
		},
		{
			icon: Users,
			titleKey: 'values.satisfaction.title',
			descriptionKey: 'values.satisfaction.description'
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
	id="values"
	class="relative py-24 lg:py-32 bg-background overflow-hidden"
>
	<!-- Background Pattern -->
	<div class="absolute inset-0 opacity-5">
		<div class="absolute top-0 left-0 w-96 h-96 bg-primary rounded-full blur-3xl"></div>
		<div class="absolute bottom-0 right-0 w-96 h-96 bg-primary rounded-full blur-3xl"></div>
	</div>

	<div class="container mx-auto px-4 sm:px-6 lg:px-8 relative z-10">
		<!-- Header -->
		<div class="text-center max-w-2xl mx-auto mb-20">
			<div
				class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-primary/10 text-primary text-sm font-medium mb-6 transition-all duration-700 {isVisible
					? 'opacity-100 translate-y-0'
					: 'opacity-0 translate-y-4'}"
			>
				{$t('values.badge')}
			</div>
			<h2
				class="text-4xl sm:text-5xl font-bold text-foreground mb-6 transition-all duration-700 delay-100 {isVisible
					? 'opacity-100 translate-y-0'
					: 'opacity-0 translate-y-8'}"
			>
				{$t('values.title')}
			</h2>
			<p
				class="text-xl text-muted-foreground leading-relaxed transition-all duration-700 delay-200 {isVisible
					? 'opacity-100 translate-y-0'
					: 'opacity-0 translate-y-8'}"
			>
				{$t('values.subtitle')}
			</p>
		</div>

		<!-- Values -->
		<div class="grid sm:grid-cols-2 lg:grid-cols-5 gap-6">
			{#each values as value, index}
				{@const Icon = value.icon}
				<div
					class="group p-6 rounded-3xl glass border border-white/5 hover:border-primary/20 hover:bg-white/5 transition-all duration-500 hover:-translate-y-2 {isVisible
						? 'opacity-100 translate-y-0'
						: 'opacity-0 translate-y-12'}"
					style="transition-delay: {index * 100}ms"
				>
					<div
						class="w-16 h-16 rounded-2xl bg-primary/10 border border-primary/20 flex items-center justify-center mx-auto mb-6 group-hover:scale-110 group-hover:bg-primary group-hover:text-white transition-all duration-500 shadow-lg"
					>
						<Icon class="w-8 h-8 transition-colors" />
					</div>
					<h3
						class="text-lg font-bold text-foreground mb-3 text-center group-hover:text-primary transition-colors"
					>
						{$t(value.titleKey)}
					</h3>
					<p
						class="text-sm text-muted-foreground leading-relaxed text-center group-hover:text-foreground/80 transition-colors"
					>
						{$t(value.descriptionKey)}
					</p>
				</div>
			{/each}
		</div>
	</div>
</section>
