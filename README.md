svelte-backtotop
====================


[![npm](https://img.shields.io/npm/v/svelte-backtotop.svg)](https://www.npmjs.com/package/svelte-backtotop)

Demos:
- _None Yet_

## How to use

1. Install

    ```
    npm install --save-dev svelte-backtotop
    ```

2. Use in a svelte component, for example `_layout.svelte`:

    ```js
    <div class="layout">
      <Navbar />
      <div class="container mt-4">
        <slot></slot>
      </div>
      <br class="last-br" />
      {#if process.browser}
        <BackToTop>
          <button class="btn btn-secondary btn-to-top" type="button">
            <Icon data={chevronUp} />
          </button>
        </BackToTop>
      {/if}
    </div>

    <script>
    import Icon from 'svelte-awesome/components/Icon'
    import chevronUp from 'svelte-awesome/icons/chevron-up'
    import Navbar from '~/components/Navbar.svelte'
    import BackToTop from 'svelte-backtotop/src/index'

    // or if you're not using any props/events:
    // import BackToTop from 'svelte-backtotop/src/components/SimpleBackToTop.svelte'

    </script>

    <style>
    .last-br {
      /* the user needs to be able to scroll back far enough to click buttons */
      /* otherwise the scroll to top button wiill block other buttons */
      padding-bottom: 10rem;
    }
    </style>
    ```


3. Further Notes:

* this is a port of https://github.com/caiofsouza/vue-backtotop which was for a non-svelte front-end framework
