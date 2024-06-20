<script lang="ts">
    import {fade} from "svelte/transition";

    export let name: string;
    export let selected: boolean;
</script>

<div class="category" class:selected>
    <div class="name">
        {name}
    </div>
</div>

<style lang="scss">
    @import "../../../../colors.scss";

    .name {
        font-weight: 400;
        color: $tabgui-text-color;
        font-size: 14px;
        width: 100%;
        padding: 7px 12px 7px 12px;
        padding-right: 50px;
        background: linear-gradient(
            to left,
            rgba(black, 0.5) 50%,
            rgba(black, 0.6) 50%
        );
        background-size: 200% 100%;
        background-position: right bottom;
        will-change: background-position;
        transition: background-position 0.2s ease-out;
        overflow: hidden;
    }

    .category {
        display: flex;

        &.selected .name {
            background-position: left bottom;
        }
    }
</style>
