<script lang="ts">
  export let isBeingDragged: boolean;

  $: console.log(isBeingDragged);
</script>

<section class="container">
  <header class="app-window-drag-handle" />
  <div>
    <iframe src="https://codesandbox.io/p/github/HasanRs/macos-web/main?import=true&embed=1&showConsole=true"
     style="width:100%; height: 100%; border:0; border-radius: 4px; overflow:hidden;"
     title="HasanRs/macos-web/main"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms disallow-modals disallow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>
  </div>
</section>

<style lang="scss">
  .container {
    background-color: #202327;
    padding: 1px;

    border-radius: inherit;

    display: grid;
    grid-template-rows: auto 1fr;
  }

  iframe {
    width: 100%;
    height: 100%;

    border-radius: 0 0 0.75rem 0.75rem;
  }

  header {
    padding: 0.9rem;
  }

  :global(.tl-container.vscode) {
    top: 0.6rem;
    left: 0.6rem;
  }
</style>
