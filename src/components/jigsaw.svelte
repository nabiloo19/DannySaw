<script>
  export let image_url;
  import { onMount } from "svelte";
  onMount(() => {
    let dali = new Image();

    dali.src = image_url;
    dali.onload = () => {
      const canvas = new headbreaker.Canvas("my-canvas", {
        preventOffstageDrag: true,
        width: 600,
        height: 500,
        pieceSize: 120,
        proximity: 10,
        borderFill: 10,
        strokeWidth: 5,
        lineSoftness: 0.12,
        fixed: true,
        strokeColor: "black",
        preventOffstageDrag: true,
        image: dali,
        outline: new headbreaker.outline.Rounded(),
      });

      canvas.adjustImagesToPuzzleHeight();

      canvas.autogenerate({
        horizontalPiecesCount: 3,
        verticalPiecesCount: 3,
      });

      // canvas.shuffleColumns(1)
      canvas.shuffleGrid();

      canvas.draw();
    };
  });
</script>

<div style="
margin: 30%;
  
border: 10px solid black

" id="my-canvas" />
