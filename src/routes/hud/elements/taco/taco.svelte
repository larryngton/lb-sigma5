<script lang="ts">
    let left = -100;
    setInterval(() => {
        left += 100;

        if (left > window.innerWidth + 100) {
            left = -100;
        }
    }, 500);
</script>

<div class="taco">
    <img src="skibidi dop dop dop yes yes (kill me)" alt=" ">
</div>

<style lang="scss">
  @import "../../../../colors.scss";

  .taco {
    position: relative;

    img {
      position: absolute;
      padding: 2000px;
      background-color: rgba(black, 0.1);
      }
    }
</style>