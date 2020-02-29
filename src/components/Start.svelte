<script>
  import { goto } from '@sapper/app';

  let onClick = e => {
    e.preventDefault();
    const hash = '#about';
    const target = document.getElementById(hash.substring(1));

    if (target) {
      e.preventDefault();
      goto(hash);
      window.scrollTo({
        top: target.offsetTop,
        behavior: 'smooth',
      });
    }
  };
</script>

<style lang="scss" src="../styles/Start.scss">

</style>

<div id="start" class="Start">
  <div
    class="Start__inner siteSidePadding fadeIn siteWidth invisibleSideScrolling">
    <a href="#about" class="Start__continueLink" on:click="{onClick}">
      <h1 class="Start__headline">Front End Web Dev</h1>
      <img src="/img/downarrow.svg" alt="About" class="Start__downArrow" />
    </a>
  </div>
</div>
