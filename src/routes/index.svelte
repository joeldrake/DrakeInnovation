<script>
  import Header from '../components/Header.svelte';
  import Start from '../components/Start.svelte';
  import About from '../components/About.svelte';
  import Work from '../components/Work.svelte';
  import Contact from '../components/Contact.svelte';

  import smoothscroll from 'smoothscroll-polyfill';
  import { onMount, onDestroy } from 'svelte';

  import throttle from 'lodash/throttle';

  let handleScrollThrottled, start, isAutoScrolling;

  const inViewPercent = 0.5;

  onMount(() => {
    handleScrollThrottled = throttle(handleScroll, 300, { leading: false });

    start = document.getElementById('start');

    smoothscroll.polyfill();

    if (window.location.hash) {
      const hash = window.location.hash.substring(1);
      const target = document.getElementById(hash);

      if (target) {
        setAutoScrolling();
        window.scrollTo({
          top: target.offsetTop,
          behavior: 'smooth',
        });
      }
    }

    addEventListeners();
  });

  onDestroy(() => {
    if (typeof window !== 'undefined') {
      removeEventListeners();
    }
  });

  const addEventListeners = () => {
    document.addEventListener('scroll', handleScrollThrottled);
    window.addEventListener('hashchange', onHashchange, false);
  };

  const removeEventListeners = () => {
    document.removeEventListener('scroll', handleScrollThrottled);
    window.addEventListener('hashchange', onHashchange, false);
  };

  const onHashchange = () => {
    setAutoScrolling();
  };

  const setAutoScrolling = () => {
    isAutoScrolling = true;
    setTimeout(() => {
      isAutoScrolling = false;
    }, 500);
  };

  const handleScroll = e => {
    const scrollTop =
      document.body.scrollTop || document.documentElement.scrollTop;

    const isScrollAboveHalfStart = start.offsetHeight / 2 > scrollTop;

    if (isScrollAboveHalfStart && window.location.hash) {
      window.history.replaceState(null, null, ' ');
    }
  };
</script>

<style>

</style>

<svelte:head>
  <title>Drake Innovation</title>
</svelte:head>

<div class="site">
  <Header />
  <Start />
  <About />
  <Work />
  <Contact />
</div>
