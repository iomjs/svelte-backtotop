{#if visible}
  <div
    transition:fade
    class="svelte-back-to-top"
    {style}
    on:click={backToTop}
  >
    <slot/>
  </div>
{/if}

<script>
import { fade } from 'svelte/transition';
import { onDestroy, onMount } from 'svelte'

// simple for when you don't need any of the optional extras

// @var String or Number
let visibleoffset = 600
// @var String or Number
let visibleoffsetbottom = 0
// @var String
let right = '30px'
// @var String
let bottom = '40px'

let visible = false
let style

$: style = `bottom:${bottom};right:${right};`

onMount(() => {
  window.smoothscroll = () => {
    let currentScroll = document.documentElement.scrollTop || document.body.scrollTop
    if (currentScroll > 0) {
      window.requestAnimationFrame(window.smoothscroll)
      window.scrollTo(0, Math.floor(currentScroll - (currentScroll / 5)))
    }
  }
  window.addEventListener('scroll', catchScroll)
})
onDestroy(() => {
  window.removeEventListener('scroll', catchScroll)
})

/**
 * Catch window scroll event
 * @return {void}
 */
function catchScroll (event) {
  const pastTopOffset = window.pageYOffset > parseInt(visibleoffset)
  const pastBottomOffset = window.innerHeight + window.pageYOffset >= document.body.offsetHeight - parseInt(visibleoffsetbottom)
  visible = parseInt(visibleoffsetbottom) > 0 ? pastTopOffset && !pastBottomOffset : pastTopOffset
}
/**
 * The function who make the magics
 * @return {void}
 */
function backToTop () {
  window.smoothscroll()
}

</script>

<style>
.svelte-back-to-top {
  cursor:pointer;
  position: fixed;
  z-index: 1000;
}
</style>
