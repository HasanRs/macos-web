<script lang="ts">
  import { theme } from '🍎/stores/theme.store';
  import TwitterIcon from '~icons/mdi/twitter';
  import BlogIcon from '~icons/mdi/grease-pencil';
  import WorksIcon from '~icons/ic/round-workspaces';
  import GithubIcon from '~icons/mdi/github';
  import DevToIcon from '~icons/mdi/dev-to';
  import { onMount } from 'svelte';

  let activeSection = 'aboutme';
  let repos = [];

  function external(node: HTMLAnchorElement) {
    node.rel = 'noopener noreferrer';
    node.target = '_blank';
  }

  function setActiveSection(section: string) {
    activeSection = section;
  }

  async function fetchRepos() {
    try {
      const response = await fetch('https://api.github.com/users/HasanRs/repos');
      if (!response.ok) {
        throw new Error(`HTTP error! Status: ${response.status}`);
      }
      repos = await response.json();
    } catch (error) {
      console.error('Error fetching repos:', error);
    }
  }

  onMount(() => {
    fetchRepos();
  });
</script>

<section class="container">
  <header class="titlebar app-window-drag-handle">
    <span>Hasan's Profile</span>
  </header>

  <aside class:light={$theme.scheme === 'light'}>
    <nav>
      <a on:click={() => setActiveSection('aboutme')}> <DevToIcon /> About me </a>
      <a on:click={() => setActiveSection('blog')}> <BlogIcon /> Blog </a>
      <a on:click={() => setActiveSection('works')}> <WorksIcon /> Works </a>
      <hr />
      <a href="https://github.com/HasanRs" use:external> <GithubIcon /> Github </a>
    </nav>
  </aside>

  <section class="content">
    {#if activeSection === 'aboutme'}
      <div id="aboutme">
        <!-- svelte-ignore a11y-img-redundant-alt -->
        <img src="https://avatars.githubusercontent.com/u/30007306?v=4" alt="Hasan's profile picture" style="width: 100px; height: 100px;" />
        <h1>Hasan</h1>
        <p>
          Hi! I'm Hasan, a software developer from Turkey. I'm passionate about web development and open-source software.
          I'm currently working on a few projects, and you can check them out on my GitHub profile.
          I also write blog posts about web development and programming in general.
          
          <br />
          <br />

          You can follow me on Twitter to stay updated on my latest projects and blog posts.

          <br />
          <br />

          <a href="https://twitter.com/HasanRs_">Follow me on Twitter <TwitterIcon /></a>

          <br />
          <br />

          If you have any questions or just want to say hi, feel free to send me an email at
          <a href="mailto:hasanbaygul@protonmail.com">mail me</a>.

          <br />
          <br />

          Thanks for visiting my profile!
        </p>
      </div>
    {/if}
    {#if activeSection === 'blog'}
      <div id="blog">
        <h1>Blog</h1>
        <p>Coming soon...</p>
      </div>
    {/if}
    {#if activeSection === 'works'}
      <div id="works">
        <h1>Works</h1>
        <ul>
          {#each repos as repo}
            <li>
              <a href={repo.html_url} target="_blank" rel="noopener noreferrer">
                <div class="repo-card">
                  <h2>{repo.name}</h2>
                  <p>{repo.description || 'No description available'}</p>
                  <span class="repo-lang">{repo.language || 'Unknown'}</span>
                </div>
              </a>
            </li>
          {/each}
        </ul>
      </div>
    {/if}
  </section>
</section>

<style lang="scss">
.container {
  --color: var(--system-color-light-hsl);

  display: grid;
  grid-template-columns: 12rem 1fr;
  grid-template-rows: 3rem 1fr;

  border-radius: inherit;

  background-image: linear-gradient(
    to right,
    hsla(var(--color), 0.7) 12rem,
    hsla(var(--color), 1) 12rem 100%
  );

  transition: --color 200ms ease-in;

  color: var(--system-color-dark);

  overflow: hidden; /* Scroll'u engeller */
}

.titlebar {
  grid-area: 1 / 1 / span 1 / span 2;

  display: flex;
  justify-content: center;

  z-index: 1;

  padding: 0.9rem 1rem;

  width: 100%;

  border-top-left-radius: inherit;
  border-top-right-radius: inherit;

  user-select: none;

  span {
    color: hsla(var(--system-color-dark-hsl), 0.8);
    font-weight: 500;
    font-size: 0.9rem;
    letter-spacing: 0.5px;
  }
}

aside {
  grid-area: 1 / 1 / span 2 / span 1;

  transform: translateZ(0);

  margin: 1.8px 0 0px 1.8px;

  border-top-left-radius: 0.5rem;
  border-bottom-left-radius: inherit;

  &::before {
    content: '';

    width: inherit;
    height: inherit;

    border-radius: inherit;

    position: fixed;
    left: 0;
    top: 0;

    z-index: -1;
    backdrop-filter: blur(12px);
  }

  &.light {
    margin: 1.7px 0 0px 1.7px;

    border-top-left-radius: 0.5rem;
    border-bottom-left-radius: 0.5rem;
  }

  nav {
    display: flex;
    flex-direction: column;
    gap: 0.2rem;

    margin: 4rem 0.6rem;

    hr {
      display: block;

      width: 100%;
      height: 1px;

      background-color: hsla(var(--system-color-dark-hsl), 0.2);

      border: none;
    }

    a {
      display: flex;
      gap: 0.4rem;
      align-items: center;

      color: hsla(var(--system-color-dark-hsl), 0.9);
      text-decoration: none;
      font-weight: 400;

      padding: 0.5rem 0.5rem;

      border-radius: 0.4rem;

      transition: background-color 100ms ease;

      &:hover {
        background-color: hsla(var(--system-color-dark-hsl), 0.2);
      }
    }
  }
}

.content {
  grid-area: 2 / 2 / span 1 / span 1;

  display: flex;
  flex-direction: column;

  padding: 1rem;

  overflow-y: auto; /* İçerikte scroll yapabilmek için */
  height: calc(100% - 1rem); /* Titlebar yüksekliğine göre ayarlanır */

  img {
    border-radius: 50%;
  }

  ul {
    list-style: none;
    padding: 0;
    margin: 0;
    display: flex;
    flex-direction: column;
    gap: 1rem;
    width: 100%;
    max-width: 600px;
  }

  li {
    background: var(--system-color-light);
    border-radius: 0.5rem;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    overflow: hidden;
    transition: transform 0.3s ease, box-shadow 0.3s ease;
    cursor: pointer;

    &:hover {
      transform: translateY(-5px);
      box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
    }

    a {
      display: block;
      color: var(--system-color-dark);
      text-decoration: none;
      padding: 1rem;
    }

    .repo-card {
      display: flex;
      flex-direction: column;
      gap: 0.5rem;
    }

    h2 {
      font-size: 1.2rem;
      margin: 0;
    }

    p {
      font-size: 0.9rem;
      margin: 0;
    }

    .repo-lang {
      font-size: 0.8rem;
      color: hsla(var(--system-color-dark-hsl), 0.6);
    }
  }
}

.emoji {
  height: 1em;
  width: 1em;

  vertical-align: middle;
}

h1 {
  font-size: 2.618rem;
  line-height: 1.618;
}

h2 {
  font-size: 1.618rem;
  line-height: 1.2;
}

p {
  line-height: 1.618rem;
}

</style>
