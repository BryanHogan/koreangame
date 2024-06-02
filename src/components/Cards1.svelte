<script lang="ts">
    import { cards as fullCards } from "../data/cards1.ts"; // Adjust the path as necessary

    const cards = shuffle(fullCards).slice(0, 5);
    let shuffledFronts = shuffle([...cards.map((card) => card.front)]);
    let shuffledBacks = shuffle([...cards.map((card) => card.back)]);

    function shuffle(array: any[]): any[] {
        for (let i = array.length - 1; i > 0; i--) {
            const j = Math.floor(Math.random() * (i + 1));
            [array[i], array[j]] = [array[j], array[i]];
        }
        return array;
    }

    function checkMatch(front: string, back: string): boolean {
        const card = cards.find((card) => card.front === front);
        return card ? card.back === back : false;
    }
    let matchedCards: string[] = [];

    let selectedFront: string | null = null;
    let selectedBack: string | null = null;
    let message: string = "";

    function selectFront(front: string) {
        selectedFront = front;
        checkSelection();
    }

    function selectBack(back: string) {
        selectedBack = back;
        checkSelection();
    }

    function checkSelection() {
        if (selectedFront && selectedBack) {
            if (checkMatch(selectedFront, selectedBack)) {
                message = "Correct match!";
                matchedCards.push(selectedFront, selectedBack);
                shuffledFronts = shuffledFronts.filter(
                    (front) => !matchedCards.includes(front),
                );
                shuffledBacks = shuffledBacks.filter(
                    (back) => !matchedCards.includes(back),
                );
            } else {
                message = "Incorrect match. Try again!";
            }
            selectedFront = null;
            selectedBack = null;
        }
    }
</script>
<h2 class="text-3xl font-bold mb-4">Match the Fronts to the Backs</h2>
<div class="grid grid-cols-2 gap-4">
    <div class="group">
        <h3 class="text-2xl font-semibold">Fronts</h3>
        {#each shuffledFronts as front}
            {#if !matchedCards.includes(front)}
                <button
                    class="btn btn-primary m-2 {selectedFront === front ? 'btn-active' : ''}"
                    on:click={() => selectFront(front)}
                    aria-label={`Select the English word ${front}`}
                >
                    {front}
                </button>
            {/if}
        {/each}
    </div>

    <div class="group">
        <h3 class="text-2xl font-semibold">Backs</h3>
        {#each shuffledBacks as back}
            {#if !matchedCards.includes(back)}
                <button
                    class="btn btn-secondary m-2 {selectedBack === back ? 'btn-active' : ''}"
                    on:click={() => selectBack(back)}
                    aria-label={`Select the Korean word ${back}`}
                >
                    {back}
                </button>
            {/if}
        {/each}
    </div>
</div>

<p class="mt-4 text-lg">{message}</p>

<style>
    .btn-active {
        transform: scale(1.05);
        font-weight: bold;
        background-color: #4ade80; /* Tailwind 'emerald-400' */
    }
</style>