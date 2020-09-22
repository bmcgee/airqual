<script>
  export let aqi;
  import { interpolateRgbBasis } from "d3-interpolate";
  import { getAQIDescription, getAQIMessage, getAQIcolor } from "./aqicalc";
</script>

<style>
  .container {
    width: 100%;
    /* height: 100%; */
    padding-top: 100%;
    position: relative;
  }
  svg {
    position: absolute;
    top: 0;
    left: 0;
    padding-left: 1vw;
  }
</style>

<div class="container">
  <svg viewbox="0 0 200 200">
    <circle cx="100" cy="100" r="100" fill={getAQIcolor(aqi)} />
    <text
      alignment-baseline="central"
      text-anchor="middle"
      fill="white"
      font-size="100"
      x="100"
      y="100">
      {aqi}
    </text>
    Sorry, your browser does not support inline SVG.
  </svg>
</div>
