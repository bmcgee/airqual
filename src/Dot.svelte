<script>
  export let aqi;
  import { interpolateRgbBasis } from "d3-interpolate";
  import { aqanduAQIFromPM, getAQIDescription, getAQIMessage } from "./aqicalc";

  let getAQIcolor = function(aqi) {
    let color = interpolateRgbBasis([
      "green",
      "yellow",
      "orange",
      "red",
      "purple",
      "purple",
      "maroon",
      "maroon",
      "maroon",
      "maroon"
    ])(aqi / 500);
    return color;
  };
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
    font-size: 20vw;
    font-family: "Lucida Sans", "Lucida Sans Regular", "Lucida Grande",
      "Lucida Sans Unicode", Geneva, Verdana, sans-serif;
  }
</style>

<div class="square" style="--bg: {getAQIcolor(aqi)}">
  <div class="content">
    <p>{aqi}</p>
  </div>

</div>
<p>{getAQIDescription(aqi)}</p>
