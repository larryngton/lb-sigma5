<script lang="ts">
    import {listen} from "../../../../integration/ws.js";
    import type {PlayerData} from "../../../../integration/types";
    import {REST_BASE} from "../../../../integration/host";
    import {fly} from "svelte/transition";
    import HealthProgress from "./HealthProgress.svelte";
    import type {TargetChangeEvent} from "../../../../integration/events";

    let target: PlayerData | null = null;
    let visible = true;

    let hideTimeout: number;

    function startHideTimeout() {
        hideTimeout = setTimeout(() => {
            visible = false;
        }, 500);
    }

    listen("targetChange", (data: TargetChangeEvent) => {
        target = data.target;
        visible = true;
        clearTimeout(hideTimeout);
        startHideTimeout();
    });

    startHideTimeout();
</script>

{#if visible && target != null}
    <div class="targethud">
        <div class="main-wrapper">
            <div class="avatar">
                <img src="{REST_BASE}/api/v1/client/resource/skin?uuid={target.uuid}" alt="avatar" />
            </div>
    
            <div class="name">{target.username}</div>
            <div class="healthpercent">
                {(Math.floor(((target.actualHealth + target.absorption) / (target.maxHealth + target.absorption)) * 100))}%
            </div>
        </div>    
        
        <HealthProgress maxHealth={target.maxHealth + target.absorption} health={target.actualHealth + target.absorption} />
    </div>
{/if}

<style lang="scss">
    @import "../../../../colors.scss";

    .targethud {
        //position: fixed;
        //top: 50%;
        left: calc(50% + 5px);
        //transform: translateY(-50%); // overwrites the component transform
        width: 270px;
        background: rgba(34,34,34, 0.9);
        overflow: hidden;
        height: 64px;
        box-shadow: 0px 0px 20px rgba(black, 0.6);
         
    }

    .main-wrapper {
        display: grid;
        grid-template-areas:
            "a b d"
            "f c e";
        padding: 7px;
    }

    .name {
        grid-area: a;
        color: $targethud-text-color;
        font-weight: 400;
        align-self: flex-start;
        padding-left: 58px;
        padding-top: 9px;
    }

    .healthpercent {
        grid-area: d;
        font-weight: 400;
        color: rgb(125,125,125);
        z-index: 1;
        align-self: flex-start;
        padding-top: 9px;
        text-align: right;
        padding-right: 5px;
    }

    .avatar {
        grid-area: a;
        height: 50px;
        width: 50px;
        position: relative;
        image-rendering: pixelated;
        background-image: url("/img/steve.png");
        background-repeat: no-repeat;
        background-size: cover;
        overflow: hidden;

        img {
            position: absolute;
            scale: 6.25;
            left: 118px;
            top: 118px;
        }
    }
</style>
