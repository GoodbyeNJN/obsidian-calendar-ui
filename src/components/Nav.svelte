<script lang="ts">
  import type { Moment } from "moment";

  import Arrow from "./Arrow.svelte";

  export let displayedMonth: Moment;
  export let today: Moment;

  export let resetDisplayedMonth: () => void;
  export let incrementDisplayedMonth: () => void;
  export let decrementDisplayedMonth: () => void;
  export let incrementDisplayedYear: () => void;
  export let decrementDisplayedYear: () => void;

  // Get the word 'Today' but localized to the current language
  const todayDisplayStr = today.calendar().split(/\d|\s/)[0];

  // eslint-disable-next-line @typescript-eslint/no-explicit-any
  let isMobile = (window.app as any).isMobile;
</script>

<div class="nav" class:is-mobile="{isMobile}">
  <h3 class="title" on:click="{resetDisplayedMonth}">
    <span class="year">{displayedMonth.format("YYYY")}</span><span class="unit">年</span><span class="month">{displayedMonth.format("M")}</span><span class="unit">月</span>
  </h3>
  <div class="right-nav">
    <Arrow
      direction="left"
      onClick="{decrementDisplayedYear}"
      tooltip="Previous Year"
    />
    <Arrow
      direction="left"
      onClick="{decrementDisplayedMonth}"
      tooltip="Previous Month"
    />
    <div class="reset-button" on:click="{resetDisplayedMonth}">
      {todayDisplayStr}
    </div>
    <Arrow
      direction="right"
      onClick="{incrementDisplayedMonth}"
      tooltip="Next Month"
    />
    <Arrow
      direction="right"
      onClick="{incrementDisplayedYear}"
      tooltip="Next Year"
    />
  </div>
</div>

<style>
  .nav {
    align-items: center;
    display: flex;
    margin: 0.6em 0 1em;
    padding: 0 6px;
    width: 100%;
  }

  .nav.is-mobile {
    padding: 0;
  }

  .title {
    color: var(--color-text-title);
    font-size: 1.5em;
    margin: 0;
  }

  .is-mobile .title {
    font-size: 1.3em;
  }

  .month {
    color: var(--interactive-accent);
    text-transform: capitalize;
  }

  .year {
    color: var(--interactive-accent);
  }

  .unit {
    padding: 0 2px;
    font-size: 0.6em;
  }

  .right-nav {
    display: flex;
    justify-content: center;
    margin-left: auto;
  }

  .reset-button {
    cursor: pointer;
    border-radius: 4px;
    color: var(--text-muted);
    font-weight: 600;
    letter-spacing: 1px;
    padding: 0px 4px;
    text-transform: uppercase;
  }

  .is-mobile .reset-button {
    display: none;
  }
</style>
