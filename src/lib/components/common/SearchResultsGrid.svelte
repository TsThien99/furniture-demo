<script lang="ts">
    import { onMount } from 'svelte';

    const fakeItems = Array(5).fill(null);
    let opacityValue = 0;

    onMount(() => {
        setTimeout(() => opacityValue = 1, 250);
    });
</script>

<div class="results-grid" style="opacity: {opacityValue}">
    {#each fakeItems as _, i}
        <div class="result-card">
            <img src={`/images/fake-items/fake-item${i + 1}.svg`} alt="product" />
        </div>
    {/each}
</div>

<style lang="scss">
    .results-grid {
        display: grid;
        grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
        gap: 2rem;
        margin-top: 1rem;
        transition: opacity 0.25s ease-in-out;

        .result-card {
            border-radius: 8px;
            overflow: hidden;
            box-shadow: 0 2px 8px rgba(0,0,0,0.1);

            img {
                width: 100%;
                height: auto;
                display: block;
            }
        }
    }
</style>