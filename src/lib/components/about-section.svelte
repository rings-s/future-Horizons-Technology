<script>
	import { onMount } from 'svelte';
	import { Eye, Target } from 'lucide-svelte';
	import { t } from 'svelte-i18n';

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
	id="about"
	class="relative py-24 lg:py-32 bg-secondary/20 overflow-hidden"
>
	<div class="container mx-auto px-4 sm:px-6 lg:px-8 relative z-10">
		<div class="grid lg:grid-cols-2 gap-16 lg:gap-24 items-center">
			<!-- Left: Image -->
			<div
				class="relative group transition-all duration-700 {isVisible
					? 'opacity-100 translate-x-0'
					: 'opacity-0 -translate-x-12'}"
			>
				<div class="relative rounded-[2.5rem] overflow-hidden border border-white/10 shadow-2xl">
					<div
						class="absolute inset-0 bg-gradient-to-br from-primary/20 via-transparent to-transparent z-10 opacity-0 group-hover:opacity-100 transition-opacity duration-500"
					></div>
					<img
						src="/about-technician.png"
						alt="Professional printer maintenance"
						class="w-full aspect-[4/3] object-cover transform group-hover:scale-105 transition-transform duration-700"
					/>
				</div>
				<div
					class="absolute -bottom-8 -right-8 w-64 h-64 bg-primary/20 rounded-full blur-3xl -z-10"
				></div>
			</div>

			<!-- Right: Content -->
			<div class="space-y-8">
				<div
					class="transition-all duration-700 delay-100 {isVisible
						? 'opacity-100 translate-x-0'
						: 'opacity-0 translate-x-12'}"
				>
					<div
						class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-primary/10 text-primary text-sm font-medium mb-6"
					>
						{$t('about.badge')}
					</div>
					<h2 class="text-4xl sm:text-5xl font-bold text-foreground mb-6">
						{$t('about.title')}
						<span class="text-transparent bg-clip-text bg-gradient-to-r from-primary to-blue-500"
							>{$t('about.titleHighlight')}</span
						>
					</h2>
					<div class="space-y-4 text-lg text-muted-foreground leading-relaxed">
						<p>{$t('about.p1')}</p>
						<p>{$t('about.p2')}</p>
					</div>
				</div>

				<div
					class="grid sm:grid-cols-2 gap-6 transition-all duration-700 delay-300 {isVisible
						? 'opacity-100 translate-y-0'
						: 'opacity-0 translate-y-8'}"
				>
					<div
						class="p-6 rounded-2xl glass border border-white/5 hover:border-primary/20 transition-all"
					>
						<div class="w-12 h-12 rounded-xl bg-primary/10 flex items-center justify-center mb-4">
							<Eye class="w-6 h-6 text-primary" />
						</div>
						<h3 class="text-lg font-bold text-foreground mb-2">{$t('about.vision.title')}</h3>
						<p class="text-sm text-muted-foreground leading-relaxed">
							{$t('about.vision.description')}
						</p>
					</div>

					<div
						class="p-6 rounded-2xl glass border border-white/5 hover:border-primary/20 transition-all"
					>
						<div class="w-12 h-12 rounded-xl bg-primary/10 flex items-center justify-center mb-4">
							<Target class="w-6 h-6 text-primary" />
						</div>
						<h3 class="text-lg font-bold text-foreground mb-2">{$t('about.mission.title')}</h3>
						<p class="text-sm text-muted-foreground leading-relaxed">
							{$t('about.mission.description')}
						</p>
					</div>
				</div>
			</div>
		</div>
	</div>
</section>
