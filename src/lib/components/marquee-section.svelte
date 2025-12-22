<script>
	const partners = [
		'Al-Quswa Schools',
		'Talgo International',
		'Future Horizons Technology',
		'Enterprise Solutions',
		'Digital Print Co',
		'Office Tech Saudi'
	];
</script>

<section
	class="py-12 overflow-hidden border-y border-white/5 bg-background/50 backdrop-blur-sm relative z-20"
>
	<div class="relative">
		<!-- Gradient masks -->
		<div
			class="absolute left-0 top-0 bottom-0 w-32 bg-gradient-to-r from-background to-transparent z-10"
		></div>
		<div
			class="absolute right-0 top-0 bottom-0 w-32 bg-gradient-to-l from-background to-transparent z-10"
		></div>

		<!-- Marquee -->
		<div class="flex animate-marquee hover:pause-animation">
			<div class="flex gap-16 pr-16">
				{#each partners as partner}
					<div class="flex items-center gap-4 group cursor-default">
						<span
							class="text-xl sm:text-2xl font-bold text-muted-foreground/40 whitespace-nowrap group-hover:text-primary/80 transition-colors duration-500"
						>
							{partner}
						</span>
						<span
							class="w-1.5 h-1.5 rounded-full bg-primary/20 group-hover:bg-primary/60 transition-colors duration-500"
						></span>
					</div>
				{/each}
			</div>
			<div class="flex gap-16 pr-16" aria-hidden="true">
				{#each partners as partner}
					<div class="flex items-center gap-4 group cursor-default">
						<span
							class="text-xl sm:text-2xl font-bold text-muted-foreground/40 whitespace-nowrap group-hover:text-primary/80 transition-colors duration-500"
						>
							{partner}
						</span>
						<span
							class="w-1.5 h-1.5 rounded-full bg-primary/20 group-hover:bg-primary/60 transition-colors duration-500"
						></span>
					</div>
				{/each}
			</div>
		</div>
	</div>
</section>

<style>
	.pause-animation:hover {
		animation-play-state: paused;
	}
</style>
