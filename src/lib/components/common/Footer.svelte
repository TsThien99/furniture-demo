<script>
    import { onMount } from 'svelte';

    // Import all brand logos
    const brands = [
        'AEG',
        'Flsk',
        'klingel',
        'Lampenwelt',
        'Obi',
        'Rituals',
        'Sofa',
        'Villeroy',
        'zubruggen',
        'AEG',
        'Flsk',
        'klingel',
        'Lampenwelt',
        'Obi',
        'Rituals',
        'Sofa',
        'Villeroy',
        'zubruggen',
    ];

    let currentIndex = 0;
    const slideStep = 140;
    const slideDuration = 3000;
    let position = 0;
    const maxSlide = brands.length * slideStep;

    onMount(() => {
        const interval = setInterval(() => {
            position = (position + slideStep) % maxSlide;
        }, slideDuration);

        return () => {
            clearInterval(interval); // Cleanup on component destruction
        };
    });
</script>

<div class="container">
    <div class="logo-container">
        <div class="logo-track" style="transform: translateX(-{position}px)">
            {#each [...brands, ...brands] as brand}
                <img src={`/images/brands/${brand}.svg`} alt={`${brand} logo`} />
            {/each}
        </div>
    </div>
</div>

<style>
    .container {
        width: 100%;
        padding: 2rem 4rem;
        overflow: hidden;
        border-radius: 0 0 3.75em 3.75em;
    }

    .logo-container {
        width: 100%;
        overflow: hidden;
    }

    .logo-track {
        display: flex;
        gap: 60px;
        transition: transform 1s linear;
        transform: translateX(0);
    }

    .logo-track img {
        object-fit: contain;
        width: 80px;
        filter: grayscale(100%) brightness(0) opacity(0.5);
    }
</style>
