<script>
  import { spring } from "svelte/motion";
  import { separator } from "./../separator.js";
  import { onMount } from "svelte";

  let windowHeight,
    // x,
    // y,
    // cw = 400,
    ch = 300,
    // rw = 300,
    rh = windowHeight,
    bluepos = spring(
      { x: 0, y: 0 },
      {
        stiffness: 1,
        damping: 1
      }
    );
  onMount(() => {
    const h = windowHeight / 2;
    bluepos = spring(
      { x: 0, y: h - 20 },
      {
        stiffness: 1,
        damping: 1
      }
    );
    ch = h - 20;
    rh = h - 20;
  });

  function blueMove(event) {
    bluepos.update($coords => ({
      x: 0,
      y: $coords.y + event.detail.dy
    }));
    // cw = event.detail.x;
    ch = event.detail.y - 10;
    rh = windowHeight - event.detail.y - 20;
    // console.log("moveY1:", event.detail.y);
  }

  function blueEnd(event) {
    // console.log("endY1:", event.detail.y);
    // coords.set({ x: 0, y: 0 });
  }
</script>

<style>
  main {
    background-color: #111;
    color: white;
  }
  .red {
    top: 0px;
    left: 0px;
    position: absolute;
    border-radius: 4px;
    background-color: #ff3e00;
    cursor: row-resize;
    overflow: auto;
    padding: 30px;
  }
  .green {
    bottom: 0px;
    left: 0px;
    position: absolute;
    border-radius: 4px;
    background-color: green;
    cursor: move;
    overflow: auto;
    padding: 30px;
  }
  #result {
    left: 0px;
    width: 100%;
    position: absolute;
    border-radius: 4px;
    background-color: blue;
    cursor: move;
  }
</style>

<svelte:window bind:innerHeight={windowHeight} />
<main>
  <div class="red" style="height:{ch}px">
    Lorem ipsum dolor sit amet, consectetur adipisicing elit. Sit nulla
    repudiandae consequatur, aperiam, dolor reprehenderit blanditiis voluptates
    eos a veniam commodi. Quibusdam ipsum molestias non culpa explicabo
    perferendis ipsam laborum mollitia ex, quam debitis temporibus numquam
    quisquam quaerat porro dolore sapiente voluptatum quia facilis? Voluptatem
  </div>

  <div
    id="result"
    use:separator
    on:panmove={blueMove}
    on:panend={blueEnd}
    style="transform: translate({$bluepos.x}px,{$bluepos.y}px)">
    Drag handler
  </div>

  <div class="green" style="height:{rh}px;">
    Lorem ipsum dolor sit amet, consectetur adipisicing elit. Sit nulla
    repudiandae consequatur, aperiam, dolor reprehenderit blanditiis voluptates
    eos a veniam commodi. Quibusdam ipsum molestias non culpa explicabo
    perferendis ipsam laborum mollitia ex, quam debitis temporibus numquam
    quisquam quaerat porro dolore sapiente voluptatum quia facilis? Voluptatem
    nostrum a, unde optio, reprehenderit laudantium cupiditate nesciunt in
    perspiciatis temporibus dolorum quo repellendus totam facere amet aut quod
    commodi delectus quisquam quas doloremque ex at! Est nulla mollitia dolores
    natus soluta in dolorum distinctio voluptatum officia omnis recusandae quas
    obcaecati, tempora repellat voluptatibus esse nobis quia commodi autem
    consectetur non. Ea impedit nemo laboriosam ut aliquid alias nisi obcaecati
    esse eveniet quisquam cumque dicta nostrum asperiores aut sapiente vel
    commodi quo eum, rerum in provident dolorem reprehenderit? Nisi expedita
    consequuntur modi impedit at doloribus tempore perferendis soluta pariatur
    deserunt iure
  </div>
</main>
