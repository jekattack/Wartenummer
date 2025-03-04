<script lang="ts">
    import { Spring } from 'svelte/motion';
    import { derived, writable } from 'svelte/store';

    export let count: number;

    const countStore = writable(count);
    const offset = derived(countStore, $count => modulo($count, 1));

    function modulo(n: number, m: number) {
        // handle negative numbers
        return ((n % m) + m) % m;
    }

    function updateCount(delta: number) {
        count += delta;
        countStore.set(count);
    }
</script>

<div class="count">
    <button onclick={() => updateCount(-1)} aria-label="Decrease the count by one">
        <svg aria-hidden="true" viewBox="0 0 1 1">
            <path d="M0,0.5 L1,0.5" />
        </svg>
    </button>

    <div class="count-viewport">
        <div class="count-digits" style="transform: translate(0, {100 * $offset}%)">
            <strong class="hidden" aria-hidden="true">{count + 1}</strong>
            <strong>{count}</strong>
        </div>
    </div>

    <button onclick={() => updateCount(1)} aria-label="Increase the count by one">
        <svg aria-hidden="true" viewBox="0 0 1 1">
            <path d="M0,0.5 L1,0.5 M0.5,0 L0.5,1" />
        </svg>
    </button>
</div>

<style>
    .count {
        display: flex;
        border-top: 1px solid rgba(0, 0, 0, 0.1);
        border-bottom: 1px solid rgba(0, 0, 0, 0.1);
        margin: 1rem 0;
    }

    .count button {
        width: 2em;
        padding: 0;
        display: flex;
        align-items: center;
        justify-content: center;
        border: 0;
        background-color: transparent;
        touch-action: manipulation;
        font-size: 2rem;
    }

    .count button:hover {
        background-color: var(--color-bg-1);
    }

    svg {
        width: 25%;
        height: 25%;
    }

    path {
        vector-effect: non-scaling-stroke;
        stroke-width: 2px;
        stroke: #444;
    }

    .count-viewport {
        width: 8em;
        height: 4em;
        overflow: hidden;
        text-align: center;
        position: relative;
    }

    .count-viewport strong {
        position: absolute;
        display: flex;
        width: 100%;
        height: 100%;
        font-weight: 400;
        color: var(--color-theme-1);
        font-size: 4rem;
        align-items: center;
        justify-content: center;
    }

    .count-digits {
        position: absolute;
        width: 100%;
        height: 100%;
    }

    .hidden {
        top: -100%;
        user-select: none;
    }
</style>
