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
        bottom: 23px;
        left: 66px;
        max-width: 72%;
        background-color: rgba($arraylist-base-color, 0.5);
    }

    .thumb {
        height: 10px;
        background-color: white;
        transition: ease width 0.5s;
        z-index: 0;
    }    
</style>