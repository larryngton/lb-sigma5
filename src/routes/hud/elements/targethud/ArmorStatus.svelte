<script lang="ts">
    import {REST_BASE} from "../../../../integration/host";
    import type {ItemStack} from "../../../../integration/types";

    export let itemStack: ItemStack;
</script>

<div class="armor-status">
    <img class="icon" src="{REST_BASE}/api/v1/client/resource/itemTexture?id={itemStack.identifier}" alt={itemStack.identifier} />
    </div>

<style lang="scss">
    @import "../../../../colors.scss";

    .armor-status {
        display: flex;
        align-items: left;
        padding-top: 5px;
        column-gap: 5px;
    }

    .icon {
        height: 30px;
        width: 30px;
        image-rendering: pixelated;
    }
</style>