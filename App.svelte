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

  //data 2nd section - investiments
  let invest_per_source;
  $: invest_per_source = iirsa_data
    .groupBy("fonte_investimento")
    .summarise({ total_invest: { investimento_total: "sum" } })
    .arrange({ total_invest: "ascending" });
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
  
      <!-- 1st section -->
        <Section
          x1={0}
          x2={1}
          y1={0.05}
          y2={0.49}
          {padding}
          flipY
          scaleX={scaleBand().domain(projects_per_year.column('fim')).padding(1)}
          scaleY={scaleLinear().domain(projects_per_year.domain('total_count')).nice()}
        >
   
          <!-- contents of 1st section -->
          <PointLayer x={projects_per_year.column('fim')} y={projects_per_year.column('total_count')} opacity={0.6} fill={"purple"} /> 
         
          <XAxis title="Ano" tickCount = {5}/>
          <YAxis title="Inversiones (USD)" />
        </Section>

        <!-- 2nd section -->
        <Section
          x1={0}
          x2={1}
          y1={0.55}
          y2={1}
          {padding}
          flipY
          scaleX={scaleBand().domain(invest_per_source.column('fonte_investimento')).padding(1)}
          scaleY={scaleLinear().domain(invest_per_source.domain('total_invest')).nice()}
        >

        <!-- contents of 2nd section -->
          <PointLayer x={invest_per_source.column('fonte_investimento')} y={invest_per_source.column('total_invest')} opacity={0.6} fill={"magenta"} /> 
         
          <XAxis title="Fuente de Inversion" tickCount = {5}/>
          <YAxis title="Inversiones (USD)" />
        </Section>
          
        
      </Graphic>
    </div>
  </div>
  
  <style>
</style>