<script lang="ts">
    import Header from './common/Header.svelte'
    import SearchGroup from './SearchGroup.svelte';
    import Footer from './common/Footer.svelte';
    import { Position } from '$lib/types/position';

    let searchGroupPlaceholderHeight: number = 0;
    function handlePositionChange(position: Position) {
        switch (position) {
            case Position.Fixed:
                {
                    searchGroupPlaceholderHeight = 56;
                    break;
                }
            case Position.Relative:
               {
                    searchGroupPlaceholderHeight = 0;
                break;
               }
        }
    }
</script>

<div class="container">
    <Header />
    <div class="title">
        <p>Die Suchmaschine für dein Zuhause</p>
    </div>
    <div class="des">
        <p>All-in-one: Suche, entdecke, vergleiche und gestalte neu mit der KI Raumgestaltung und visueller Suche.</p>
    </div>
    <div class="search-group-placeholder" style="height: {searchGroupPlaceholderHeight}px"></div>
    <SearchGroup onPositionChange={handlePositionChange} />
    <div class="background-image-placeholder"></div>
    <Footer />
</div>

<style lang="scss">
    .container {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        width: 90%;
        border-radius: 3.75em;
        box-shadow: 0px 2px 30px 2px rgba(0, 0, 0, 0.2);
        background-color: #F2F2F2;
        max-width: 1240px;
        padding: 0 1rem;
        background-image: url('/images/couch.png');
        background-repeat: no-repeat;
        background-position: right 65%;
        background-size: 20em;
        .title {
            width: 90%;
            p {
                font-size: 3em;
                color: #155252;
                font-weight: 700;
                line-height: 1.1;
                letter-spacing: 1%;
            }
        }

        .des {
            margin-top: 1.5em;
            width: 90%;
            margin-bottom: 3rem;
            p {
                max-width: 50%;
                line-height: 1.5;
                letter-spacing: 1%;
                font-size: 1.25em;
                color: #1B2B2B;
                font-weight: 400;
            }
        }


        .background-image-placeholder {
            height: 5em;
        }
    }

    // Media queries
    @media (max-width: 1024px) {
        .container {
            width: 100%;
            border-radius: 0 0 2.75em 2.75em;
            background-image: none;
            .title {
                max-width: 100%;
                margin-bottom: 3rem;
                p {
                    font-size: 2em;
                    text-align: center;
                }
            }
            .des {
                display: none;

            }
        }
        .background-image-placeholder {
            display: none;
        }

    }

</style>