<script>
	import { onMount } from 'svelte';
	import { Quote, Star } from 'lucide-svelte';
	import { t } from 'svelte-i18n';

	const clients = [
		{
			nameKey: 'clients.alquswa.name',
			sectorKey: 'clients.alquswa.sector',
			testimonialKey: 'clients.alquswa.testimonial',
			image: '/client-alquswa-logo.png'
		},
		{
			nameKey: 'clients.talgo.name',
			sectorKey: 'clients.talgo.sector',
			testimonialKey: 'clients.talgo.testimonial',
			image: '/client-talgo-logo.png'
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
	id="clients"
	class="relative py-24 lg:py-32 bg-background overflow-hidden"
>
	<div class="container mx-auto px-4 sm:px-6 lg:px-8 relative z-10">
		<!-- Header -->
		<div class="text-center max-w-3xl mx-auto mb-20">
			<div
				class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-primary/10 text-primary text-sm font-medium mb-6 transition-all duration-700 {isVisible
					? 'opacity-100 translate-y-0'
					: 'opacity-0 translate-y-4'}"
			>
				{$t('clients.badge')}
			</div>
			<h2
				class="text-4xl sm:text-5xl font-bold text-foreground mb-6 transition-all duration-700 delay-100 {isVisible
					? 'opacity-100 translate-y-0'
					: 'opacity-0 translate-y-8'}"
			>
				{$t('clients.title')}
			</h2>
			<p
				class="text-xl text-muted-foreground leading-relaxed transition-all duration-700 delay-200 {isVisible
					? 'opacity-100 translate-y-0'
					: 'opacity-0 translate-y-8'}"
			>
				{$t('clients.subtitle')}
			</p>
		</div>

		<!-- Clients Grid -->
		<div class="grid md:grid-cols-2 gap-8 lg:gap-12">
			{#each clients as client, index}
				<div
					class="group relative p-10 rounded-[2.5rem] glass border border-white/5 hover:border-primary/20 transition-all duration-500 hover:-translate-y-2 {isVisible
						? 'opacity-100 translate-y-0'
						: 'opacity-0 translate-y-12'}"
					style="transition-delay: {index * 200}ms"
				>
					<Quote
						class="absolute top-10 right-10 w-12 h-12 text-primary/10 group-hover:text-primary/20 transition-colors"
					/>

					<div class="flex items-center gap-6 mb-8">
						<div
							class="w-20 h-20 rounded-2xl overflow-hidden bg-white/5 border border-white/10 shadow-lg group-hover:scale-105 transition-transform duration-500"
						>
							<img
								src={client.image || '/placeholder.svg'}
								alt={$t(client.nameKey)}
								class="w-full h-full object-cover"
							/>
						</div>
						<div>
							<h3
								class="text-xl font-bold text-foreground group-hover:text-primary transition-colors"
							>
								{$t(client.nameKey)}
							</h3>
							<p class="text-sm text-muted-foreground mt-1">{$t(client.sectorKey)}</p>
							<div class="flex gap-1 mt-2">
								{#each [1, 2, 3, 4, 5] as i}
									<Star class="w-3 h-3 fill-current text-yellow-500" />
								{/each}
							</div>
						</div>
					</div>

					<p class="text-lg text-muted-foreground leading-relaxed italic relative z-10">
						"{$t(client.testimonialKey)}"
					</p>
				</div>
			{/each}
		</div>

		<!-- Trust Badge -->
		<div
			class="mt-20 text-center transition-all duration-700 delay-500 {isVisible
				? 'opacity-100 translate-y-0'
				: 'opacity-0 translate-y-8'}"
		>
			<div
				class="inline-flex items-center gap-3 px-8 py-4 rounded-full glass border border-white/10 hover:bg-white/5 transition-colors"
			>
				<span class="relative flex h-3 w-3">
					<span
						class="animate-ping absolute inline-flex h-full w-full rounded-full bg-primary opacity-75"
					></span>
					<span class="relative inline-flex rounded-full h-3 w-3 bg-primary"></span>
				</span>
				<span class="text-sm font-medium text-foreground/80">
					{$t('clients.badge2')}
				</span>
			</div>
		</div>
	</div>
</section>
