<script>
  import { scaleLinear, scaleBand, scaleTime } from "d3-scale";
  import { iirsa } from "./iirsa.js";
  import {
    Graphic,
    Section,
    RectangleLayer,
    PointLayer,
    Line,
    XAxis,
    YAxis
  } from "@snlab/florence";
  import DataContainer from "@snlab/florence-datacontainer";

  // overall settings
  const padding = { left: 80, bottom: 40, top: 5, right: 5 };

  // aux variables
  let selected_country = "";
  let aux = "";
  let tempo = [
    "2000",
    "2001",
    "2002",
    "2003",
    "2004",
    "2005",
    "2006",
    "2005",
    "2007",
    "2008",
    "2009",
    "2010",
    "2011",
    "2012",
    "2013",
    "2014",
    "2015",
    "2016",
    "2017",
    "2018",
    "2019",
    "2020"
  ];

  // entire dataset
  let iirsa_data = new DataContainer(iirsa);
  const iirsa_data_raw = new DataContainer(iirsa);

  //selection logic
  $: if (selected_country == "") {
    iirsa_data = iirsa_data_raw;
  } else {
    iirsa_data = iirsa_data_raw.filter(row => row.pais == selected_country);
  }

  // data for interaction
  const countries = iirsa_data.domain("pais");
  $: console.log(selected_country);

  //data 1st section - investiments
  let projects_per_year;
  $: projects_per_year = iirsa_data
    .groupBy("fim")
    .summarise({ total_count: { investimento_total: "sum" } })
    .arrange({ fim: "ascending" });
  //.mutate({ date_as_date: row => new Date(row.fim) });
</script>
  
  <label for="country_select">Seleccionar Pais:</label>
    <select name="country" id="country_select" bind:value={selected_country}>
      <option value="">Seleccionar Pais</option>
      {#each countries as country} 
        <option value={country}>{country}</option>
      {/each}
    </select>  
  
  
  <div class="graph">
    <div class="main-chart">
      <!-- main chart -->
      <Graphic width={825} height={825}>
  
      <!-- contents of 1st section -->
        <Section
          x1={0}
          x2={0.49}
          y1={0}
          y2={0.49}
          {padding}
          flipY
          scaleX={scaleBand().domain(projects_per_year.column('fim')).padding(1)}
          scaleY={scaleLinear().domain(projects_per_year.domain('total_count'))}
        >
   
          <!-- contents of 1st section -->
          <PointLayer x={projects_per_year.column('fim')} y={projects_per_year.column('total_count')} opacity={0.6} fill={"purple"} />
  
  
          <XAxis title="Ano" tickCount = {5}/>
          <YAxis title="Inversiones (USD)" />
        </Section>
      </Graphic>
    </div>
  </div>
  
  <style>
</style>