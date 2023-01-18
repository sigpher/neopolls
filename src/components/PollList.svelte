<script>
    import { fade, slide, scale } from "svelte/transition";
    import { flip } from "svelte/animate";
    import PollDetails from "./PollDetails.svelte";
    import PollStore from "../stores/PollStore";
    export let polls = [];

    PollStore.subscribe((data) => {
        polls = data;
    });
</script>

<div class="poll-list">
    {#each polls as poll (poll.id)}
        <div in:fade out:scale|local animate:flip={{ duration: 500 }}>
            <PollDetails {poll} />
        </div>
    {:else}
        <h3>Click Add New Poll to add an new poll</h3>
    {/each}
</div>

<style>
    .poll-list {
        display: grid;
        grid-template-columns: 1fr 1fr;
        grid-gap: 20px;
    }
    h3 {
        color: #d91b42;
        margin: 0 auto;
    }
</style>
