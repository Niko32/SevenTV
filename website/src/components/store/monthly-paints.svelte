<script lang="ts">
	import { faEllipsisV, faRepeat } from "@fortawesome/pro-regular-svg-icons";
	import StoreSection from "./store-section.svelte";
	import Fa from "svelte-fa";
	import PaintPreview from "../paint-preview.svelte";
</script>

<StoreSection title="Monthly Paints">
    <div class="buttons" slot="header">
        <div class="renew-countdown">
            <Fa icon={faRepeat} size="1.2x" />
            <span>12 d</span>
        </div>
        <button class="button secondary square">
            <Fa icon={faEllipsisV} size="1.2x" fw />
        </button>
    </div>
    {#each Array(2) as _}
        <PaintPreview />
    {/each}
</StoreSection>

<style lang="scss">
    .buttons {
        display: flex;
        align-items: center;
        gap: 0.75rem;
    }

    .renew-countdown {
        display: flex;
        align-items: center;
        gap: 0.5rem;
        white-space: nowrap;

        color: var(--text-lighter);
        font-size: 0.75rem;
    }
</style>
