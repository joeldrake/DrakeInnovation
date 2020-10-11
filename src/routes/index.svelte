<script>
  import Header from '../components/Header.svelte';
  import Start from '../components/Start.svelte';
  import About from '../components/About.svelte';
  import Work from '../components/Work.svelte';
  import Contact from '../components/Contact.svelte';

  import smoothscroll from 'smoothscroll-polyfill';
  import { onMount, onDestroy } from 'svelte';

  import throttle from 'lodash/throttle';

  let handleScrollThrottled, start;
  const serverSide = typeof window === 'undefined';

  onMount(() => {
    handleScrollThrottled = throttle(handleScroll, 300, { leading: false });

    start = document.getElementById('start');

    smoothscroll.polyfill();

    if (window.location.hash) {
      const hash = window.location.hash.substring(1);
      const target = document.getElementById(hash);

      if (target) {
        window.scrollTo({
          top: target.offsetTop,
          behavior: 'smooth',
        });
      }
    }

    addEventListeners();
  });

  onDestroy(() => {
    removeEventListeners();
  });

  const addEventListeners = () => {
    if (serverSide) return;
    document.addEventListener('scroll', handleScrollThrottled);
  };

  const removeEventListeners = () => {
    if (serverSide) return;
    document.removeEventListener('scroll', handleScrollThrottled);
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
