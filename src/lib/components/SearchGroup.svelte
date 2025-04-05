<script lang="ts">
    import SearchOverlay from './SearchOverlay.svelte';
    import { onMount } from 'svelte';
    import { Position } from '$lib/types/position';

    export let onPositionChange: (position: Position) => void;

    let isOverlayOpen = false;
    let searchWrapperElement: HTMLElement;
    let wrapperInitialReact: DOMRect;
    let isFixed = false;
    let isActiveOverlay = false;
    let wrapperTop = 0;
    let wrapperLeft = 0;

    onMount(() => {
        wrapperInitialReact = searchWrapperElement.getBoundingClientRect();
        wrapperLeft = wrapperInitialReact.left / 2;
        wrapperTop = wrapperInitialReact.top;
    });

    function handleStarsClick(event: MouseEvent) {
        event.stopPropagation();
    }

    function handleScannerClick(event: MouseEvent) {
        event.stopPropagation();
    }

    function handleWrapperClick() {
        if (searchWrapperElement) {
            isOverlayOpen = true;
            setTimeout(() => {
                isFixed = true;
                isActiveOverlay = true;
                wrapperLeft = 0;
                wrapperTop = 0;
                onPositionChange(Position.Fixed);
            }, 0);
        }
    }

    function handleKeydown(e: KeyboardEvent) {
        if (e.target === e.currentTarget && (e.key === 'Enter' || e.key === ' ')) {
            handleWrapperClick();
        }
    }


    function handleSearchIconClick(event: MouseEvent) {
        if (isOverlayOpen) {
            event.stopPropagation();
            closeOverlay();
        }
    }

    const closeOverlay = () => {
        isOverlayOpen = false;
        wrapperLeft = wrapperInitialReact.left / 2;
        wrapperTop = wrapperInitialReact.top;
        isActiveOverlay = false;
        setTimeout(() => {
            isFixed = false;
            onPositionChange(Position.Relative);
        }, 375);
    };

    const handleInput = (element: HTMLInputElement) => {
        element.focus({ preventScroll: true });
    };
</script>

<div
    bind:this={searchWrapperElement}
    class="search-wrapper"
    class:fixed-position={isFixed}
    class:active-overlay={isActiveOverlay}
    style="top: {wrapperTop}px; left: {wrapperLeft}px; cursor: {isOverlayOpen ? 'default' : 'pointer'};"
    on:click={handleWrapperClick}
    on:keydown={handleKeydown}
    tabindex="0"
    role="button"
    aria-label="Search"
>
    <div class="search-container">
        <button class="search-icon" on:click={handleSearchIconClick}>
            {#if isOverlayOpen}
                <img src="/images/icons/arrow-left.svg" alt="back" />
            {:else}
                <img src="/images/icons/search-line-orange.svg" alt="search" />
            {/if}
        </button>



        {#if isOverlayOpen}
        <input
            use:handleInput
            type="text"
            placeholder="Suchen"
            class="search-input"
        />
        {:else}
            <div class="placeholder">
                <p class="title">Ich suche nach</p>
                <p class="des">z.B. Grünes Sofa unter 500 Euro</p>
            </div>
        {/if}

        <div class="buttons">
            <button class="green-button button start-btn" on:click={handleStarsClick}>
                <img src="/images/icons/stars.svg" alt="stars icon" />
            </button>
            <button class="green-button button" on:click={handleScannerClick}>
                <img src="/images/icons/scanner.svg" alt="scanner" />
            </button>
        </div>
    </div>

</div>
<SearchOverlay isOpen={isOverlayOpen} onClose={closeOverlay} />

<style lang="scss">
    .search-wrapper {
        width: 90%;
        transition: all 0.375s ease-in-out;
        z-index: 2;
        padding: 0;

        &.fixed-position {
            position: fixed;
        }
        &.active-overlay {
            padding: 1rem 0.5rem;
            width: 100vw;
            background-color: #F2F2F2;

            .search-container {
                height: 48px;
                .search-icon {
                    padding: 0 0.5rem;
                }
                .buttons .green-button {
                    background-color: white;
                    outline: none;
                    img {
                        filter: invert(1);
                    }
                }
            }
        }

        .search-container {
            position: relative;
            display: flex;
            align-items: center;
            background: white;
            border-radius: 50px;
            padding: 0.5rem;
            box-shadow: 0 2px 15px rgba(0, 0, 0, 0.15);
            height: 56px;
            z-index: 2;

            .search-icon {
                padding: 0 1rem;
                display: flex;
                align-items: center;
                background-color: white;
                border: none;
                cursor: pointer;
                img {
                    width: 24px;
                    height: 24px;
                }
            }

            .search-input {
                flex: 1;
                border: none;
                outline: none;
                font-size: 1rem;
                padding: 0.5rem;
            }

            .placeholder {
                flex: 1;

                p {
                    width: fit-content;
                    line-height: 1.1;
                    cursor: pointer;
                }

                .title {
                    font-size: 0.875em;
                    color: #1B2B2B;
                    font-weight: 400;
                }

                .des {
                    font-size: 0.625em;
                    color: #BFBFBF;
                }
            }

            .buttons {
                display: flex;
                gap: 0.5em;

                button {
                    border-radius: 50%;
                    padding: 0.5em;

                    img {
                        width: 24px;
                        height: 24px;
                    }
                }
            }
        }

        @media (max-width: 1024px) {
            .start-btn {
                display: none;
            }
        }
    }
</style>