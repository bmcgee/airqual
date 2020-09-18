<script>
  import purpleair from "purpleair";
  import { interpolateRgbBasis } from "d3-interpolate";

  const purple = (async () => {
    //closer one
    //hill dr 56109
    var sensor = await purpleair.getSensor(56109);
    var aqi = await purpleair.getAQI(sensor);
    var aqiClass = await purpleair.getAQIClass(aqi);

    console.log(aqi);
    let data = {
      aqi: await purpleair.getAQI(sensor),
      aqiClass: await purpleair.getAQIClass(aqi)
    };

    console.log(data);

    return await data;
  })();

  let getAQIcolor = function(c) {
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
    ])(c / 500);
    return color;
  };
</script>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }
  div > p {
    font-size: 30vw;
  }
  p {
    font-size: 10vw;
    font-family: "Lucida Sans", "Lucida Sans Regular", "Lucida Grande",
      "Lucida Sans Unicode", Geneva, Verdana, sans-serif;
  }
  div {
    /* height: 5em;
	width: 5em; */
    margin: auto;
    width: 70vw;
    height: 70vw;
    border-radius: 50%;
    background-color: var(--bg);
    display: flex;
    justify-content: center; /* align horizontal */
    align-items: center; /* align vertical */
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>

<main>
  {#await purple}
    <p>...waiting</p>
  {:then data}
    <div style="--bg: {getAQIcolor(data.aqi)}">
      <p>{data.aqi}</p>
    </div>
    <p>{data.aqiClass}</p>

  {:catch error}
    <p>error</p>
  {/await}
</main>
