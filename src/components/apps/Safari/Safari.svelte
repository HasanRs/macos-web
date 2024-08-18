<script lang="ts">
  // TypeScript kodlarınızı buraya ekleyebilirsiniz
</script>

<section class="container">
  <header class="app-window-drag-handle">
    <input type="text" placeholder="Search..." value="🔒 https://youtube.com/NeverGonnaGiveYouUp!" />
  </header>
  <div class="video-container">
    <!-- svelte-ignore a11y-missing-attribute -->
    <iframe 
      src="https://www.youtube.com/embed/dQw4w9WgXcQ?autoplay=1" 
      frameborder="0" 
      allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" 
      allowfullscreen
			style="height: 35vh;">
    </iframe>
		<div class="video-info">
			<h1 class="video-title">Rick Astley - Never Gonna Give You Up</h1>
			<p class="video-description">Rick Astley's iconic song, popular since 1987. Don't forget to listen!</p>
    </div>
  </div>
</section>

<style lang="scss">
  header {
    padding: 1rem;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .container {
    height: 100%;
    width: 100%;
    background-color: hsla(0, 0%, 27%, 0.7);
    backdrop-filter: blur(40px);
    border-radius: inherit;
    display: grid;
    grid-template-rows: auto auto 1fr;
    font-family: var(--system-font-family) !important;
  }

  input[type="text"] {
    border: none;
    border-radius: 8px;
    padding: 0.5rem 1rem;
    font-size: 0.8rem;
    background-color: rgba(255, 255, 255, 0.1);
    color: #fff;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
    outline: none;
    transition: box-shadow 0.3s ease;
    height: 20px;
    width: 60%;
    text-align: center;

    &::placeholder {
      color: #888;
    }

    &:focus {
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.3);
    }
  }

  .video-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 1rem;
    height: 100%;
    width: 100%;

    iframe {
      width: 80%;
      max-width: 800px;
      height: 450px;
      border-radius: 8px;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.3);
			pointer-events: none;
    }
  }

  .video-info {
    text-align: center;
    margin-top: 1rem;
    color: #fff;

    .video-title {
      font-size: 1.5rem;
      margin-bottom: 0.5rem;
    }

    .video-description {
      font-size: 0.9rem;
    }
  }
</style>
