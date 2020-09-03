<script>
  import { goto } from '@sapper/app';

  let navToggle,
    addedEventListeners = false;
  let onClickNavLink = e => {
    if (addedEventListeners) {
      navToggle.checked = false;
      removeEventListeners();
    }
  };

  let navToggleToggle = e => {
    if (navToggle.checked) {
      addEventListeners();
    } else {
      removeEventListeners();
    }
  };

  const addEventListeners = () => {
    if (!addedEventListeners) {
      addedEventListeners = true;
      document.addEventListener('click', handleClick);
    }
  };

  const removeEventListeners = () => {
    addedEventListeners = false;
    document.removeEventListener('click', handleClick);
  };

  const handleClick = async e => {
    const target = e.target;
    var isHeader__nav = target.closest('.Header__nav');
    if (!isHeader__nav) {
      navToggle.checked = false;
      window.requestAnimationFrame(() => {
        removeEventListeners();
      });
    }
  };
</script>

<style lang="scss" src="../styles/Header.scss">

</style>

<header class="Header">

  <div class="Header__inner siteWidth siteSidePadding">
    <div class="Header__logo">Joel Drake</div>

    <input
      type="checkbox"
      id="navToggle"
      bind:this="{navToggle}"
      on:change="{navToggleToggle}"
      class="Header__nav-button"
      aria-label="Open navigation" />
    <label class="Header__nav-toggle" for="navToggle">
      <img src="/img/menu.svg" class="Header__nav-open" alt="Open navigation" />
      <img
        src="/img/close.svg"
        class="Header__nav-close"
        alt="Close navigation" />
    </label>

    <nav class="Header__nav animateUnderline" aria-haspopup="true">
      <a href="#about" on:click="{onClickNavLink}">About 🐲</a>
      <a href="#work" on:click="{onClickNavLink}">Work 🛠</a>
      <a href="#contact" on:click="{onClickNavLink}">Contact 📨</a>
    </nav>
  </div>

</header>
