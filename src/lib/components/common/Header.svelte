<script>
    import { goto } from '$app/navigation';
</script>

<div class="container">
    <div class="logo">
        <img src="/images/icons/logo.svg" alt="InteriorTrends" on:click={() => goto('/')} />
    </div>

    <nav>
        <button class="green-button button">
            <img src="/images/icons/stars.svg" alt="stars icon" />
            <span>KI Wohnideen</span>
        </button>

        <div class="nav-items">
            <button class="nav-item">
                <img src="/images/icons/search-line.svg" alt="search" />
                <span>Suche</span>
            </button>

            <button class="nav-item">
                <img src="/images/icons/compass.svg" alt="compass" />
                <span>Wohnideen</span>
            </button>

            <button class="nav-item">
                <img src="/images/icons/heart-line.svg" alt="heart" />
                <span>Wunschliste</span>
            </button>
        </div>
    </nav>
</div>

<style>
    .container {
        display: flex;
        width: 100%;
        border-radius: 3.75em 3.75em 0 0;
        justify-content: space-between;
        align-items: center;
        padding: 2rem 4rem;
    }

    .logo img {
        height: 60px;
        cursor: pointer;
    }

    nav {
        display: flex;
        align-items: center;
        gap: 2rem;
    }

    .nav-items {
        display: flex;
        gap: 1.5rem;
    }

    .nav-item {
        display: flex;
        align-items: center;
        gap: 0.5rem;
        background: none;
        border: none;
        cursor: pointer;
        position: relative;
        &:hover {
            span {
                color: var(--text-highlight);
            }
        }
    }

    .nav-item img {
        height: 24px;
    }

    .nav-item span {
        color: #333;
        transition: color 0.25s ease-in-out;
    }

    @media (max-width: 1024px) {
        .container {
            justify-content: center;
            nav {
                display: none;
            }
            .logo img {
                height: 40px;
            }
        }
    }
</style>