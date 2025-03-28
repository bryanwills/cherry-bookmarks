<script lang="ts">
  type Modifier =
    | 'v0'
    | 'v1'
    | 'icon'
    | 'minimal'
    | 'circular'
    // padding
    | 'p5'
    | 'warn';

  interface Props {
    type?: 'reset' | 'submit' | 'button' | null;
    modifier?: Modifier[] | null;
    // native tooltip
    title?: string | null;
    disabled?: boolean;
    style?: string | null;
    icon?: import('svelte').Snippet;
    children?: import('svelte').Snippet;
    onclick?: any;
  }

  let {
    type = null,
    modifier = null,
    title = null,
    disabled = false,
    style = null,
    icon,
    children,
    onclick,
  }: Props = $props();
</script>

<button {disabled} {type} {title} {style} class={modifier ? modifier.join(' ') : ''} {onclick}>
  {#if icon}
    <span class="btn-icon">
      {@render icon?.()}
    </span>
  {/if}
  {@render children?.()}
</button>

<style lang="scss">
  button {
    --fg: var(--color-text);
    --bg: var(--bg-btn);
    --shadow: 0 0 0 3px rgba(66, 153, 225, 0.6);
    position: relative;
    appearance: none;
    outline: none;
    user-select: none;
    cursor: pointer;
    display: inline-flex;
    align-items: center;
    justify-content: center;
    padding: 10px 14px;
    font-size: 16px;
    color: var(--fg);
    background-color: var(--bg);
    border: 1px solid var(--color-btn-bo);
    border-radius: 100px;
    border-color: hsl(0deg 0% var(--bo-lightness));
    &:hover {
      border-color: hsl(0deg 0% var(--bo-lightness-hover));
      background-color: var(--bg-hover);
    }
    @media (prefers-color-scheme: dark) {
      --bo-lightness: 30%;
      --bo-lightness-hover: 70%;
      --bg-hover: hsl(0deg 0% 19%);
    }
    @media (prefers-color-scheme: light) {
      --bo-lightness: 80%;
      --bo-lightness-hover: 15%;
      --bg-hover: hsl(0deg 0% 90%);
    }
    &:active {
      transform: scale(0.99) translateY(1%);
    }
    &.circular {
      padding: 5px;
    }
    &.p5 {
      padding: 5px;
    }
    &.warn {
      background-color: hsl(351deg 77% 42% / 76%);
      border-color: rgb(246, 187, 196);
      color: #f1f1f1;
      &:hover {
        background-color: hsl(351deg 77% 42%);
      }
    }
    &.minimal {
      border-color: transparent;
      background: none;
      border: none;
      &:hover {
        background-color: var(--bg-hover);
      }
    }
    &:focus {
      box-shadow: var(--shadow);
    }
  }

  button:disabled {
    opacity: 0.5;
    cursor: not-allowed;
    &:hover {
      color: var(--fg);
      background-color: var(--bg);
      border-color: hsl(0deg 0% var(--bo-lightness));
    }
  }

  .icon {
    padding: 7px;
  }

  .v0,
  .dark {
    --bo-lightness: 30%;
    --bo-lightness-hover: 70%;
    --fg: #ddd;
    --bg: hsl(0deg 0% 5%);
    --bg-hover: hsl(0deg 0% 19%);
  }
  .v1,
  .light {
    --bo-lightness: 50%;
    --bo-lightness-hover: 15%;
    --fg: #222;
    --bg: hsl(0deg 0% 100%);
    --bg-hover: hsl(0deg 0% 90%);
  }

  .btn-icon {
    margin-right: 5px;
    display: inline-flex;
    align-items: center;
    justify-content: center;
  }
</style>
