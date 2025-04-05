<script>
    import WelcomeSection from '$lib/components/WelcomeSection.svelte';
</script>

<div class="container">
    <WelcomeSection />
</div>

<style>
    .container {
        width: 100vw;
        margin: 4em 0;
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    @media (max-width: 1024px) {
        .container {
            margin: 0;
        }
    }
</style>