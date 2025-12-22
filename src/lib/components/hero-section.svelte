<script lang="ts">
	import { onMount } from 'svelte';
	import { ArrowRight, Play, ShieldCheck, Activity } from 'lucide-svelte';
	import { t, locale } from 'svelte-i18n';
	import { fade, fly } from 'svelte/transition';

	let mounted = $state(false);
	let scrollY = $state(0);
	let mouseX = $state(0);
	let mouseY = $state(0);

	onMount(() => {
		mounted = true;
	});

	function handleMouseMove(event: MouseEvent) {
		// Smooth damping for mouse movement could be added here for extra polish
		mouseX = (event.clientX / window.innerWidth - 0.5) * 2; // -1 to 1
		mouseY = (event.clientY / window.innerHeight - 0.5) * 2; // -1 to 1
	}
</script>

<svelte:window bind:scrollY onmousemove={handleMouseMove} />

<section class="relative min-h-[110vh] flex items-center overflow-hidden bg-[#030712] text-white">
	<!-- ambient background effects -->
	<div class="absolute inset-0 z-0">
		<!-- Animated Gradient Mesh -->
		<div
			class="absolute top-[-20%] left-[-10%] w-[80vw] h-[80vw] bg-primary/20 rounded-full blur-[120px] mix-blend-screen animate-pulse-slow"
			style="transform: translate({mouseX * -20}px, {mouseY * -20}px)"
		></div>
		<div
			class="absolute bottom-[-20%] right-[-10%] w-[60vw] h-[60vw] bg-blue-600/20 rounded-full blur-[100px] mix-blend-screen animate-pulse-slow delay-1000"
			style="transform: translate({mouseX * 20}px, {mouseY * 20}px)"
		></div>

		<!-- Tech Grip Overlay -->
		<div
			class="absolute inset-0 opacity-[0.05]"
			style="background-image: linear-gradient(rgba(255, 255, 255, 0.05) 1px, transparent 1px), linear-gradient(90deg, rgba(255, 255, 255, 0.05) 1px, transparent 1px); background-size: 50px 50px; transform: perspective(1000px) rotateX(60deg) translateY({scrollY *
				0.2}px);"
		></div>

		<!-- Noise Texture -->
		<div
			class="absolute inset-0 opacity-[0.03] pointer-events-none mix-blend-overlay noise-bg"
		></div>
	</div>

	<div class="container mx-auto px-4 sm:px-6 lg:px-8 relative z-10 pt-20">
		<div class="grid lg:grid-cols-12 gap-16 items-center">
			<!-- Left Content area -->
			<div class="lg:col-span-7 space-y-10 relative">
				<!-- Pill Badge -->
				<div
					class="inline-flex items-center gap-3 px-5 py-2.5 rounded-full border border-white/5 bg-white/5 backdrop-blur-md shadow-xl transition-all hover:bg-white/10 hover:border-primary/30 group cursor-default"
				>
					<span class="relative flex h-2.5 w-2.5">
						<span
							class="animate-ping absolute inline-flex h-full w-full rounded-full bg-primary opacity-75"
						></span>
						<span class="relative inline-flex rounded-full h-2.5 w-2.5 bg-primary"></span>
					</span>
					<span
						class="text-sm font-mono tracking-wider text-primary/80 group-hover:text-primary transition-colors"
						>EST. 2025</span
					>
					<span class="w-[1px] h-4 bg-white/10"></span>
					<span class="text-sm font-medium tracking-wide text-gray-200">{$t('hero.badge')}</span>
				</div>

				<!-- Main Headline -->
				<div class="relative space-y-2">
					<!-- "Future" - Solid Heavy -->
					<div class="overflow-visible">
						<h1
							class="font-black text-white transition-all
							{$locale === 'ar'
								? 'text-5xl sm:text-6xl lg:text-7xl xl:text-8xl leading-normal scale-100'
								: 'text-6xl sm:text-7xl lg:text-8xl xl:text-9xl tracking-tighter leading-[0.85]'}"
						>
							<span
								class="block transform transition-transform duration-700 ease-out {mounted
									? 'translate-y-0'
									: 'translate-y-full'}"
							>
								{$t('hero.title1')}
							</span>
						</h1>
					</div>

					<!-- "Horizons" - Outline & Gradient Hybrid -->
					<div class="overflow-visible relative">
						<h1
							class="font-black transition-all pr-4
							{$locale === 'ar'
								? 'text-5xl sm:text-6xl lg:text-7xl xl:text-8xl leading-normal'
								: 'text-6xl sm:text-7xl lg:text-8xl xl:text-9xl tracking-tighter leading-[0.85] italic'}"
						>
							<span
								class="block text-transparent bg-clip-text bg-gradient-to-r from-primary via-blue-400 to-primary bg-300% animate-gradient transform transition-transform duration-700 delay-100 ease-out {mounted
									? 'translate-y-0'
									: 'translate-y-full'}"
							>
								{$t('hero.title2')}
							</span>

							<!-- decorative outline duplicate behind (Hidden in Arabic) -->
							{#if $locale !== 'ar'}
								<span
									class="absolute top-0 left-0 -z-10 text-transparent stroke-text opacity-30 transform transition-transform duration-700 delay-150 ease-out {mounted
										? 'translate-x-4 translate-y-0'
										: 'translate-x-0 translate-y-full'}"
									aria-hidden="true"
								>
									{$t('hero.title2')}
								</span>
							{/if}
						</h1>
					</div>

					<!-- "Technology" - Mono Technical -->
					<div class="overflow-hidden pt-2">
						<h1
							class="text-3xl sm:text-4xl lg:text-5xl font-mono font-bold tracking-widest text-gray-500 uppercase flex items-center gap-4"
						>
							<span class="w-12 h-[2px] bg-primary/50 hidden sm:block"></span>
							<span
								class="block transform transition-transform duration-700 delay-200 ease-out {mounted
									? 'translate-y-0'
									: 'translate-y-full'}"
							>
								{$t('hero.title3')}
							</span>
						</h1>
					</div>

					<!-- Abstract decoration line -->
					<div
						class="absolute top-4 bottom-4 w-[1px] bg-gradient-to-b from-transparent via-primary/30 to-transparent hidden xl:block
						{$locale === 'ar' ? '-right-8' : '-left-8'}"
					></div>
				</div>

				<p
					class="text-lg sm:text-xl text-gray-400 max-w-2xl leading-relaxed transition-all duration-700 delay-300 {mounted
						? 'opacity-100 translate-y-0'
						: 'opacity-0 translate-y-4'} 
					{$locale === 'ar' ? 'border-r border-white/10 pr-6' : 'border-l border-white/10 pl-6'}"
				>
					{$t('hero.description')}
				</p>

				<!-- Buttons -->
				<div
					class="flex flex-col sm:flex-row gap-6 pt-4 transition-all duration-700 delay-500 {mounted
						? 'opacity-100 translate-y-0'
						: 'opacity-0 translate-y-4'}"
				>
					<button
						class="group relative h-14 px-8 rounded-2xl bg-primary text-primary-foreground font-semibold text-lg overflow-hidden transition-all hover:scale-[1.02] active:scale-95 shadow-lg shadow-primary/20"
					>
						<div
							class="absolute inset-0 bg-gradient-to-r from-transparent via-white/20 to-transparent translate-x-[-100%] group-hover:animate-shimmer z-10"
						></div>
						<div class="relative z-20 flex items-center gap-3">
							{$t('hero.cta1')}
							<ArrowRight class="w-5 h-5 transition-transform group-hover:translate-x-1" />
						</div>
					</button>

					<button
						class="group h-14 px-8 rounded-2xl glass-strong border border-white/5 hover:border-white/20 text-white font-medium text-lg transition-all hover:bg-white/5 active:scale-95 flex items-center gap-3 backdrop-blur-xl"
					>
						<div
							class="w-8 h-8 rounded-full bg-white/10 flex items-center justify-center group-hover:scale-110 transition-transform"
						>
							<Play class="w-4 h-4 fill-white text-white" />
						</div>
						{$t('hero.cta2')}
					</button>
				</div>
			</div>

			<!-- Right Visual Area 3D -->
			<div
				class="lg:col-span-5 relative perspective-[2000px] h-[600px] hidden lg:flex items-center justify-center z-20"
			>
				<!-- Main Card Container -->
				<div
					class="relative w-full aspect-[4/5] max-w-md transform-style-3d transition-transform duration-100 ease-out"
					style="transform: rotateY({mouseX * 12}deg) rotateX({mouseY * -12}deg);"
				>
					<!-- Holographic Glow Behind -->
					<div
						class="absolute inset-0 bg-primary/30 rounded-[3rem] blur-[80px] -z-10 animate-pulse-slow"
					></div>

					<!-- Main Glass Card -->
					<div
						class="absolute inset-0 rounded-[3rem] glass-strong border border-white/10 overflow-hidden shadow-2xl backdrop-blur-md group"
					>
						<!-- Scanner Effect -->
						<div
							class="absolute top-0 left-0 w-full h-[2px] bg-primary/50 shadow-[0_0_20px_rgba(var(--primary),0.5)] z-20 animate-scan"
						></div>

						<!-- Image -->
						<img
							src="/hero-device.png"
							alt="Future Tech Device"
							class="absolute inset-0 w-full h-full object-cover scale-110 transition-transform duration-[2s] group-hover:scale-100"
						/>

						<!-- Overlay Gradient -->
						<div
							class="absolute inset-0 bg-gradient-to-t from-black/90 via-black/20 to-transparent"
						></div>

						<!-- Content inside card -->
						<div class="absolute bottom-0 left-0 right-0 p-8 transform translate-z-20">
							<div class="flex items-center justify-between mb-4">
								<div class="flex items-center gap-2">
									<div class="w-2 h-2 rounded-full bg-green-500 animate-pulse"></div>
									<span class="text-xs font-mono text-green-400 uppercase tracking-widest"
										>System Online</span
									>
								</div>
								<div
									class="px-2 py-1 rounded bg-white/10 text-[10px] font-mono border border-white/10 backdrop-blur-md"
								>
									V 2.5.0
								</div>
							</div>
							<h3 class="text-2xl font-bold text-white mb-1">Smart Print Hub</h3>
							<p class="text-sm text-gray-400">Next-gen management systems</p>
						</div>
					</div>

					<!-- Floating Widgets (Parallax) -->
					<!-- Widget 1: Top Right -->
					<div
						class="absolute -top-12 -right-12 p-5 rounded-3xl glass-strong border border-white/10 shadow-2xl transform-style-3d animate-float"
						style="transform: translateZ(80px) translateX({mouseX * -40}px);"
					>
						<div class="flex items-center gap-4">
							<div
								class="w-12 h-12 rounded-2xl bg-gradient-to-br from-primary to-blue-600 flex items-center justify-center shadow-lg shadow-primary/25"
							>
								<Activity class="w-6 h-6 text-white" />
							</div>
							<div>
								<div class="text-xs text-gray-400 uppercase tracking-wider mb-1">Efficiency</div>
								<div class="text-2xl font-bold text-white">98.5%</div>
							</div>
						</div>
					</div>

					<!-- Widget 2: Bottom Left -->
					<div
						class="absolute -bottom-10 -left-12 p-5 rounded-3xl glass-strong border border-white/10 shadow-2xl transform-style-3d animate-float-delayed"
						style="transform: translateZ(60px) translateX({mouseX * 40}px);"
					>
						<div class="flex items-center gap-4">
							<div
								class="w-12 h-12 rounded-2xl bg-[#1e293b] flex items-center justify-center border border-white/5"
							>
								<ShieldCheck class="w-6 h-6 text-green-400" />
							</div>
							<div>
								<div class="text-xs text-gray-400 uppercase tracking-wider mb-1">Security</div>
								<div class="text-2xl font-bold text-white">Active</div>
							</div>
						</div>
					</div>
				</div>
			</div>
		</div>
	</div>
</section>

<style>
	.glass-strong {
		background: rgba(255, 255, 255, 0.03);
		backdrop-filter: blur(20px);
		-webkit-backdrop-filter: blur(20px);
	}

	.transform-style-3d {
		transform-style: preserve-3d;
	}

	.bg-300\% {
		background-size: 300% auto;
	}

	.noise-bg {
		background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noiseFilter'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.65' numOctaves='3' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noiseFilter)' opacity='0.1'/%3E%3C/svg%3E");
	}

	@keyframes shimmer {
		100% {
			transform: translateX(100%);
		}
	}

	.animate-gradient {
		animation: gradient 6s linear infinite;
	}

	@keyframes gradient {
		0% {
			background-position: 0% 50%;
		}
		50% {
			background-position: 100% 50%;
		}
		100% {
			background-position: 0% 50%;
		}
	}

	.animate-float {
		animation: float 6s ease-in-out infinite;
	}

	.animate-float-delayed {
		animation: float 6s ease-in-out infinite 3s;
	}

	@keyframes float {
		0% {
			transform: translateZ(80px) translateY(0px);
		}
		50% {
			transform: translateZ(80px) translateY(-20px);
		}
		100% {
			transform: translateZ(80px) translateY(0px);
		}
	}

	.animate-pulse-slow {
		animation: pulse-slow 8s ease-in-out infinite;
	}

	@keyframes pulse-slow {
		0%,
		100% {
			opacity: 0.5;
			transform: scale(1);
		}
		50% {
			opacity: 0.8;
			transform: scale(1.1);
		}
	}

	.animate-scan {
		animation: scan 4s linear infinite;
	}

	@keyframes scan {
		0% {
			top: 0%;
			opacity: 0;
		}
		10% {
			opacity: 1;
		}
		90% {
			opacity: 1;
		}
		100% {
			top: 100%;
			opacity: 0;
		}
	}

	.stroke-text {
		-webkit-text-stroke: 1px rgba(255, 255, 255, 0.3);
		color: transparent;
	}
</style>
