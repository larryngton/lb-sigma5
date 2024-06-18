<script lang="ts">
    export let maxHealth: number;
    export let health: number;

    let width = Math.ceil(health / maxHealth * 100);
    $: width = Math.ceil(health / maxHealth * 100);
</script>

<div class="health-progress">
    <div class="thumb" style="width: {width}%;"></div>
</div>

<style lang="scss">
    @import "../../../../colors.scss";

    .health-progress {
        position: relative;
        bottom: 0px;
        left: 0px;
        border-radius: 0px;
        max-width: 100%;
    }

    .thumb {
        height: 14px;
        background-color: red;
        transition: ease width 0.5s;
        border-radius: 0px;
    }
</style>