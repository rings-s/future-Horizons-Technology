<script>
	import { onMount } from 'svelte';
	import { ArrowRight, Check, Star } from 'lucide-svelte';
	import { t } from 'svelte-i18n';

	const products = [
		{
			categoryKey: 'products.multifunction.category',
			titleKey: 'products.multifunction.title',
			descriptionKey: 'products.multifunction.description',
			image: '/product-multifunction.png',
			featuresKeys: [
				'products.multifunction.feature1',
				'products.multifunction.feature2',
				'products.multifunction.feature3',
				'products.multifunction.feature4'
			]
		},
		{
			categoryKey: 'products.consumables.category',
			titleKey: 'products.consumables.title',
			descriptionKey: 'products.consumables.description',
			image: '/product-consumables.png',
			featuresKeys: [
				'products.consumables.feature1',
				'products.consumables.feature2',
				'products.consumables.feature3',
				'products.consumables.feature4'
			]
		},
		{
			categoryKey: 'products.parts.category',
			titleKey: 'products.parts.title',
			descriptionKey: 'products.parts.description',
			image: '/printer-parts.png',
			featuresKeys: [
				'products.parts.feature1',
				'products.parts.feature2',
				'products.parts.feature3',
				'products.parts.feature4'
			]
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
	id="products"
	class="relative py-24 lg:py-32 bg-background overflow-hidden"
>
	<div class="container mx-auto px-4 sm:px-6 lg:px-8 relative z-10">
		<!-- Header -->
		<div class="flex flex-col lg:flex-row lg:items-end justify-between gap-8 mb-16">
			<div class="max-w-2xl">
				<div
					class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-primary/10 text-primary text-sm font-medium mb-6 transition-all duration-700 {isVisible
						? 'opacity-100 translate-y-0'
						: 'opacity-0 translate-y-4'}"
				>
					{$t('products.badge')}
				</div>
				<h2
					class="text-4xl sm:text-5xl font-bold text-foreground mb-4 transition-all duration-700 delay-100 {isVisible
						? 'opacity-100 translate-y-0'
						: 'opacity-0 translate-y-8'}"
				>
					{$t('products.title')}
				</h2>
			</div>
			<div
				class="transition-all duration-700 delay-200 {isVisible
					? 'opacity-100 translate-x-0'
					: 'opacity-0 translate-x-8'}"
			>
				<button
					class="group flex items-center gap-2 px-6 py-3 rounded-full border border-border hover:border-primary/50 hover:bg-secondary/50 transition-all duration-300"
				>
					<span class="font-medium">{$t('products.viewAll')}</span>
					<ArrowRight class="w-4 h-4 group-hover:translate-x-1 transition-transform" />
				</button>
			</div>
		</div>

		<!-- Products Grid -->
		<div class="grid lg:grid-cols-3 gap-8">
			{#each products as product, index}
				<div
					class="group relative rounded-[2rem] overflow-hidden bg-card border border-border hover:border-primary/50 transition-all duration-500 hover:shadow-2xl hover:shadow-primary/5 {isVisible
						? 'opacity-100 translate-y-0'
						: 'opacity-0 translate-y-12'}"
					style="transition-delay: {index * 150}ms"
				>
					<!-- Image Container -->
					<div class="aspect-[4/3] overflow-hidden relative">
						<div
							class="absolute inset-0 bg-gradient-to-t from-background via-transparent to-transparent z-10 opacity-60"
						></div>
						<img
							src={product.image || '/placeholder.svg'}
							alt={$t(product.titleKey)}
							class="w-full h-full object-cover group-hover:scale-110 transition-transform duration-700"
						/>

						<!-- Floating Category Badge -->
						<div
							class="absolute top-4 left-4 z-20 px-3 py-1 rounded-full glass-strong text-xs font-medium text-foreground backdrop-blur-md border border-white/10"
						>
							{$t(product.categoryKey)}
						</div>
					</div>

					<!-- Content -->
					<div class="p-8 relative z-20 -mt-12">
						<div
							class="p-6 rounded-2xl glass-strong border border-white/5 shadow-lg backdrop-blur-xl bg-background/80"
						>
							<h3
								class="text-xl font-bold text-foreground mb-2 group-hover:text-primary transition-colors"
							>
								{$t(product.titleKey)}
							</h3>
							<p class="text-sm text-muted-foreground mb-6">{$t(product.descriptionKey)}</p>

							<div class="space-y-3">
								{#each product.featuresKeys as featureKey}
									<div class="flex items-center gap-3 text-sm text-muted-foreground/80">
										<div
											class="w-5 h-5 rounded-full bg-primary/10 flex items-center justify-center shrink-0"
										>
											<Check class="w-3 h-3 text-primary" />
										</div>
										{$t(featureKey)}
									</div>
								{/each}
							</div>

							<div class="mt-6 pt-6 border-t border-border flex items-center justify-between">
								<div class="flex -space-x-2">
									{#each [1, 2, 3] as i}
										<div
											class="w-8 h-8 rounded-full border-2 border-background bg-secondary flex items-center justify-center text-[10px] font-bold"
										>
											<Star class="w-3 h-3 fill-current text-yellow-500" />
										</div>
									{/each}
								</div>
								<span class="text-xs font-medium text-primary cursor-pointer hover:underline">
									{$t('products.viewDetails')}
								</span>
							</div>
						</div>
					</div>
				</div>
			{/each}
		</div>
	</div>
</section>
