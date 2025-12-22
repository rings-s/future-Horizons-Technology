<script lang="ts">
	import { onMount } from 'svelte';
	import { TrendingUp, Users, Clock, ThumbsUp } from 'lucide-svelte';
	import { t } from 'svelte-i18n';

	let isVisible = $state(false);
	let sectionRef: HTMLElement | undefined;
	let countersStarted = $state(false);

	const stats = [
		{
			icon: TrendingUp,
			valueKey: 'stats.devices.value',
			labelKey: 'stats.devices.label',
			descriptionKey: 'stats.devices.description'
		},
		{
			icon: Users,
			valueKey: 'stats.clients.value',
			labelKey: 'stats.clients.label',
			descriptionKey: 'stats.clients.description'
		},
		{
			icon: Clock,
			valueKey: 'stats.support.value',
			labelKey: 'stats.support.label',
			descriptionKey: 'stats.support.description'
		},
		{
			icon: ThumbsUp,
			valueKey: 'stats.satisfaction.value',
			labelKey: 'stats.satisfaction.label',
			descriptionKey: 'stats.satisfaction.description'
		}
	];

	onMount(() => {
		const observer = new IntersectionObserver(
			([entry]) => {
				if (entry.isIntersecting) {
					isVisible = true;
					countersStarted = true;
				}
			},
			{ threshold: 0.3 }
		);

		if (sectionRef) {
			observer.observe(sectionRef);
		}

		return () => observer.disconnect();
	});
</script>

<section
	bind:this={sectionRef}
	class="relative py-24 lg:py-32 bg-gradient-to-b from-background to-secondary/20 overflow-hidden"
>
	<!-- Background Pattern -->
	<div class="absolute inset-0 opacity-30">
		<div
			class="absolute top-10 left-10 w-72 h-72 bg-primary/10 rounded-full blur-3xl animate-pulse"
		></div>
		<div
			class="absolute bottom-10 right-10 w-96 h-96 bg-blue-500/10 rounded-full blur-3xl animate-pulse delay-1000"
		></div>
	</div>

	<div class="container mx-auto px-4 sm:px-6 lg:px-8 relative z-10">
		<div class="grid sm:grid-cols-2 lg:grid-cols-4 gap-8">
			{#each stats as stat, index}
				{@const Icon = stat.icon}
				<div
					class="text-center p-8 rounded-3xl glass hover:glass-strong border border-white/5 transition-all duration-500 hover:-translate-y-2 {isVisible
						? 'opacity-100 translate-y-0'
						: 'opacity-0 translate-y-12'}"
					style="transition-delay: {index * 100}ms"
				>
					<div
						class="w-16 h-16 mx-auto mb-6 rounded-2xl bg-primary/10 flex items-center justify-center group-hover:scale-110 transition-transform"
					>
						<Icon class="w-8 h-8 text-primary" />
					</div>
					<div
						class="text-5xl font-bold text-foreground mb-3 bg-clip-text text-transparent bg-gradient-to-r from-foreground to-primary"
					>
						{$t(stat.valueKey)}
					</div>
					<div class="text-lg font-semibold text-foreground mb-2">{$t(stat.labelKey)}</div>
					<div class="text-sm text-muted-foreground">{$t(stat.descriptionKey)}</div>
				</div>
			{/each}
		</div>
	</div>
</section>
