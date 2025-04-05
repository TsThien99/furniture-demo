<script lang="ts">
    import SearchResultsGrid from './common/SearchResultsGrid.svelte';
    import { fade } from 'svelte/transition';

    export let isOpen = false;
    export let onClose: () => void;

    const popularSearches = Array(7).fill('Option');
</script>

{#if isOpen}
<div class="overlay">
    <div class="overlay-header">
        <div class="search-placeholder"></div>
    </div>

    <div class="search-content" in:fade={{ duration: 500 }}>
        <h2>Beliebte Suchanfragen</h2>
        <div class="popular-searches">
            {#each popularSearches as search}
                <button class="option-tag">{search}</button>
            {/each}
        </div>

        <h2>Produkte und Inspirationen</h2>
        <SearchResultsGrid />
    </div>
</div>
{/if}

<style lang="scss">
    .overlay {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100vh;
        z-index: 1;
        overflow-y: auto;
        background-color: white;
    }

    .search-placeholder {
        height: 48px;
    }

    .overlay-header {
        padding: 1rem 0.5rem;
    }

    .search-content {
        padding: 2rem;
        background: white;
        h2 {
            margin: 2rem 0 1rem;
            color: #2F4F4F;
        }
    }

    .popular-searches {
        display: flex;
        gap: 1rem;
        flex-wrap: wrap;

        .option-tag {
            padding: 0.5rem 1rem;
            border-radius: 20px;
            background: #f5f5f5;
            border: none;
            cursor: pointer;
        }
    }

    @media (max-width: 1024px) {
        .overlay-header {
            padding: 1rem 0;

            .right {
                width: 100%;
                padding: 0 1rem;
            }

            .left,
            .close,
            .right .recent-searches {
                display: none;
            }
        }
    }
</style>