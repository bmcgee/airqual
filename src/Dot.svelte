<script>
  export let aqi;
  import { interpolateRgbBasis } from "d3-interpolate";
  import { getAQIDescription, getAQIMessage, getAQIcolor } from "./aqicalc";

</script>

<style>
  .square {
    /* height: 5em;
	width: 5em; */
    margin: auto;
    width: 80%;
    /* height: 80%; */
    border-radius: 50%;
    background-color: var(--bg);
    display: flex;
    justify-content: center; /* align horizontal */
    align-items: center; /* align vertical */
  }
  .square:after {
    content: "";
    display: block;
    padding-bottom: 100%;
  }
  .content {
    position: absolute;
    /* width: 100%;
    height: 100%; */
    font-size: 40%;
    font-family: "Lucida Sans", "Lucida Sans Regular", "Lucida Grande",
      "Lucida Sans Unicode", Geneva, Verdana, sans-serif;
  }
  .container {
    width: 100%;
    /* height: 100%; */
    padding-top:100%;
    position:relative;
  }
  svg {
    position:absolute; 
    top: 0; 
    left: 0;
    padding-left: 1vw;
  }
</style>

<div class="container">
  <svg viewbox="0 0 200 200">
    <circle cx="100" cy="100" r="100" fill={getAQIcolor(aqi)} />
    <text alignment-baseline="central" text-anchor="middle" fill="white" font-size="100"  x="100" y="100">{aqi}</text>
  Sorry, your browser does not support inline SVG.
  </svg>
</div>

<!-- <svg width="200" height = 200>
  <circle cx="100" cy="100" fill="#1f77b4" r="100"></circle>
  <text fill="white" x="100" y="100" font-size="120" >A</text>

</svg> -->

<!-- <div class="square" style="--bg: {getAQIcolor(aqi)}">
  <div class="content">
    <p>{aqi}</p>
  </div>

</div> -->
