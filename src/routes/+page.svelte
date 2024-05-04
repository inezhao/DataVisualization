<!-- page.svelte -->
<!-- svelte-ignore a11y-mouse-events-have-key-events -->
<!-- svelte-ignore a11y-no-static-element-interactions -->

<script>
// @ts-nocheck
    import Years from './Years.svelte';

    import shoppingData from './shopping.json';
    const BusinessUnitShare = shoppingData.BusinessUnitShare;
    const CategoryShare = shoppingData.CategoryShare;
    const Type = shoppingData.Type;
    const Quantities = shoppingData.Quantities;
    const BusinessUnit = shoppingData.BusinessUnit;

    const widthSize = 250;
    const heightSize = 300;
    const xPos = 300;
    const yPos = 400;
    const Hspacing = 10;
    const Vspacing = 10;
    const StrokeWidth = 4.5;

    const verticalBarSize = 40;
    const verticalBarWidth = 20;

    const textSizeTitle = 20;
    const textSizeCategory = 13;

    const AdvFill = '#7fc3a4';
    const LuxFill = '#a975b5';
    const ComFill = '#657db7';

    const ArmsArmourStroke = '#de6673';
    const AdventuringEquipmentStroke = '#559f87';
    const ToolsKitsStroke = '#ff9f41';
    const PotionsScrollsStroke = '#8ff281';
    const AnimalsTransportStroke ='#ffcb39';
    const JewelryStroke = '#5dbfe1';
    const SummoningDeviceStroke = '#d43db7';
    const MusicalInstrumentStroke = '#1668c2';

    const legendBox = 20;

    const categoryShareOpacity = 0.8;
    const Opacity = 0.6;

    let hovered = '';
    function startHover(val) {
      hovered = val;
    }
    function endHover() {
      hovered = '';
    }


</script>
  
<h2>Graph title</h2>
<style>
  rect{
    fill: blue;
  }
  text{
    font-family:'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    fill:black;
    stroke:black;}
</style>


<!--Shopping Bag-->
<svg width=1700 height=700 style="background-color:#daebf1">

  <g transform="translate(150, 50)">
    <!-- Title -->
    <text x={20} y={30} fill="black" font-size={textSizeTitle} >
      Proportion of Orders</text>
      <text x={20} y={52} fill="black" font-size={textSizeTitle-2} >
        by Product Types and Business Units</text>

    <!--First 0-2 Arms & Armour-->
    <text x={xPos- 115 -verticalBarSize} y={yPos + heightSize*CategoryShare[0]/2}
    font-size={textSizeCategory}>{Type[0]}</text>
    <!--First 0-2 Arms & Armour CategoryShare-->
    <!-- svelte-ignore a11y-no-static-element-interactions -->
    <!-- svelte-ignore a11y-mouse-events-have-key-events -->
    <rect x={xPos -verticalBarSize}
    y={yPos}
    width={(verticalBarWidth)}
    height={heightSize*CategoryShare[0]}
    style="fill:{ArmsArmourStroke};stroke:{ArmsArmourStroke};stroke-width:{StrokeWidth};
    fill-opacity:{hovered == 'ARMS & ARMOUR' ? 1: categoryShareOpacity};stroke-opacity:0.9"
      on:mouseover={() => startHover('ARMS & ARMOUR')}
      on:mouseout={endHover}>
    <title>{100*CategoryShare[0]}%</title>
    </rect>
    {#if hovered=='ARMS & ARMOUR'}
      <g transform="translate(700)">
        <Years prType={hovered}/>
      </g>
    {/if}
    <!--First 0-2 Arms & Armour BusinessUnits-->
      <rect x={xPos}
      y={yPos}
      width={(widthSize*BusinessUnitShare[0])}
      height={heightSize*CategoryShare[0]}
      style="fill:{AdvFill};stroke:{ArmsArmourStroke};stroke-width:{StrokeWidth};
      fill-opacity:{Opacity};stroke-opacity:0.9" >
      <title>{100*BusinessUnitShare[0]}%</title>
      </rect>

      <rect x={xPos  + (widthSize*BusinessUnitShare[0]) + Hspacing }
      y={yPos}
      width={(widthSize*BusinessUnitShare[1])}
      height={heightSize*CategoryShare[1]}
      style="fill:{ComFill};stroke:{ArmsArmourStroke};stroke-width:{StrokeWidth};fill-opacity:{Opacity};stroke-opacity:0.9">>
      <title>{BusinessUnitShare[1]}</title>
      </rect>
        
      <rect x={xPos  + (widthSize*BusinessUnitShare[0]) + (widthSize*BusinessUnitShare[1]) + 2*Hspacing }
      y={yPos}
      width={(widthSize*BusinessUnitShare[2])}
      height={heightSize*CategoryShare[2]}
      style="fill:{LuxFill};stroke:{ArmsArmourStroke};stroke-width:{StrokeWidth};fill-opacity:{Opacity};stroke-opacity:0.9">>
      <title>{BusinessUnitShare[2]}</title>
      </rect>

    <!--Second 3-5 Adventuring Equipment-->
    <text x={xPos-170-verticalBarSize} y={yPos + heightSize*CategoryShare[3] - heightSize*CategoryShare[0] - Vspacing}
      font-size={textSizeCategory}>{Type[3]}</text>
    <!--Second 3-5 Adventuring Equipment CategoryShare-->
    <!-- svelte-ignore a11y-no-static-element-interactions -->
    <!-- svelte-ignore a11y-mouse-events-have-key-events -->
    <rect x={xPos - verticalBarSize}
    y={yPos - heightSize*CategoryShare[3] - Vspacing}
    width={(verticalBarWidth)}
    height={heightSize*CategoryShare[3]}
    style="fill:{AdventuringEquipmentStroke};stroke:{AdventuringEquipmentStroke};stroke-width:{StrokeWidth};
    fill-opacity:{hovered == 'ADVENTURING EQUIPMENT'? 1.0: categoryShareOpacity};stroke-opacity:0.9"
      on:mouseover={() => startHover('ADVENTURING EQUIPMENT')}
      on:mouseout={endHover}>
    <title>{CategoryShare[3]}</title>
    </rect>
    {#if hovered=='ADVENTURING EQUIPMENT'}
      <g transform="translate(700)">
        <Years prType={hovered}/>
      </g>
    {/if}
    <!--Second 3-5 Adventuring Equipment BusinessUnits-->
    <rect x={xPos}
    y={yPos - heightSize*CategoryShare[3] - Vspacing}
    width={(widthSize*BusinessUnitShare[3])}
    height={heightSize*CategoryShare[3]}
    style="fill:{AdvFill};stroke:{AdventuringEquipmentStroke};stroke-width:{StrokeWidth};fill-opacity:{Opacity};stroke-opacity:0.9">
    <title>{BusinessUnitShare[3]}</title>
    </rect>

    <rect x={xPos  + (widthSize*BusinessUnitShare[3]) + Hspacing }
    y={yPos - heightSize*CategoryShare[4] - Vspacing}
    width={(widthSize*BusinessUnitShare[4])}
    height={heightSize*CategoryShare[4]}
    style="fill:{ComFill};stroke:{AdventuringEquipmentStroke};stroke-width:{StrokeWidth};fill-opacity:{Opacity};stroke-opacity:0.9">>
    <title>{BusinessUnitShare[4]}</title>
    </rect>
      
    <rect x={xPos + (widthSize*BusinessUnitShare[3]) + (widthSize*BusinessUnitShare[4]) + 2*Hspacing}
    y={yPos - heightSize*CategoryShare[5] - Vspacing}
    width={(widthSize*BusinessUnitShare[5])}
    height={heightSize*CategoryShare[5]}
    style="fill:{LuxFill};stroke:{AdventuringEquipmentStroke};stroke-width:{StrokeWidth};fill-opacity:{Opacity};stroke-opacity:0.9">>
    <title>{BusinessUnitShare[5]}</title>
    </rect>

    <!--Third 6-8 Tools & Kits-->
    <text x={xPos-90-verticalBarSize} y={yPos + heightSize*CategoryShare[6]/2 - heightSize*CategoryShare[0] - Vspacing} 
    fill="black" font-size={textSizeCategory}>{Type[6]}</text>
    <!--Third 6-8 Tools & Kits CategoryShare-->
    <!-- svelte-ignore a11y-no-static-element-interactions -->
    <!-- svelte-ignore a11y-mouse-events-have-key-events -->
    <rect x={xPos- verticalBarSize}
    y={yPos - heightSize*CategoryShare[3] - heightSize*CategoryShare[6] -  2*Vspacing}
    width={(verticalBarWidth)}
    height={heightSize*CategoryShare[6]}
    style="fill:{ToolsKitsStroke};stroke:{ToolsKitsStroke};stroke-width:{StrokeWidth};
    fill-opacity:{hovered == 'TOOLS & KITS'? 1.0: categoryShareOpacity};stroke-opacity:0.9"
      on:mouseover={() => startHover('TOOLS & KITS')}
      on:mouseout={endHover}>
    <title>{CategoryShare[6]}</title>
    </rect>
    {#if hovered=='TOOLS & KITS'}
      <g transform="translate(700)">
        <Years prType={hovered}/>
      </g>
    {/if}
    <!--Third 6-8 Tools & Kits BusinessUnit-->
    <rect x={xPos}
    y={yPos - heightSize*CategoryShare[3] - heightSize*CategoryShare[6] -  2*Vspacing}
    width={(widthSize*BusinessUnitShare[6])}
    height={heightSize*CategoryShare[6]}
    style="fill:{AdvFill};stroke:{ToolsKitsStroke};stroke-width:{StrokeWidth};fill-opacity:{Opacity};stroke-opacity:0.9">
    <title>{BusinessUnitShare[6]}</title>
    </rect>

    <rect x={xPos  + (widthSize*BusinessUnitShare[6]) + Hspacing }
    y={yPos - heightSize*CategoryShare[3] - heightSize*CategoryShare[7] -  2*Vspacing}
    width={(widthSize*BusinessUnitShare[7])}
    height={heightSize*CategoryShare[7]}
    style="fill:{ComFill};stroke:{ToolsKitsStroke};stroke-width:{StrokeWidth};fill-opacity:{Opacity};stroke-opacity:0.9">>
    <title>{BusinessUnitShare[7]}</title>
    </rect>
      
    <rect x={xPos + (widthSize*BusinessUnitShare[6]) + (widthSize*BusinessUnitShare[7]) + 2*Hspacing }
    y={yPos - heightSize*CategoryShare[3] - heightSize*CategoryShare[8] -  2*Vspacing}
    width={(widthSize*BusinessUnitShare[8])}
    height={heightSize*CategoryShare[8]}
    style="fill:{LuxFill};stroke:{ToolsKitsStroke};stroke-width:{StrokeWidth};fill-opacity:{Opacity};stroke-opacity:0.9">
    <title>{BusinessUnitShare[8]}</title>
    </rect>

    <!--Fourth 9-11 Potions & Scrolls-->
    <text x={xPos-130-verticalBarSize} y={yPos + 4 + heightSize*CategoryShare[9] - heightSize*CategoryShare[0] - heightSize*CategoryShare[3] + Vspacing}
          fill="black" font-size={textSizeCategory}>{Type[9]}</text>
    <!--Fourth 9-11 Potions & Scrolls CategoryShare-->
    <!-- svelte-ignore a11y-mouse-events-have-key-events -->
    <!-- svelte-ignore a11y-no-static-element-interactions -->
    <rect x={xPos - verticalBarSize}
    y={yPos - heightSize*CategoryShare[3] - heightSize*CategoryShare[6] - heightSize*CategoryShare[9]-  3*Vspacing}
    width={(verticalBarWidth)}
    height={heightSize*CategoryShare[9]}
    style="fill:{PotionsScrollsStroke};stroke:{PotionsScrollsStroke};stroke-width:{StrokeWidth};
    fill-opacity:{hovered == 'POTIONS & SCROLLS'? 1.0: categoryShareOpacity};stroke-opacity:0.9"
      on:mouseover={() => startHover('POTIONS & SCROLLS')}
      on:mouseout={endHover}>
    <title>{CategoryShare[9]}</title>
    </rect>
    {#if hovered=='POTIONS & SCROLLS'}
      <g transform="translate(700)">
        <Years prType={hovered}/>
      </g>
    {/if}
    <!--Fourth 9-11 Potions & Scrolls BusinessUnit-->
    <rect x={xPos}
    y={yPos - heightSize*CategoryShare[3] - heightSize*CategoryShare[6] - heightSize*CategoryShare[9]-  3*Vspacing}
    width={(widthSize*BusinessUnitShare[9])}
    height={heightSize*CategoryShare[9]}
    style="fill:{AdvFill};stroke:{PotionsScrollsStroke};stroke-width:{StrokeWidth};fill-opacity:{Opacity};stroke-opacity:0.9">
    <title>{BusinessUnitShare[9]}</title>
    </rect>

    <rect x={xPos  + (widthSize*BusinessUnitShare[9]) + Hspacing }
    y={yPos - heightSize*CategoryShare[3] - heightSize*CategoryShare[6] - heightSize*CategoryShare[9]-  3*Vspacing}
    width={(widthSize*BusinessUnitShare[10])}
    height={heightSize*CategoryShare[10]}
    style="fill:{ComFill};stroke:{PotionsScrollsStroke};stroke-width:{StrokeWidth};fill-opacity:{Opacity};stroke-opacity:0.9">>
    <title>{BusinessUnitShare[10]}</title>
    </rect>
      
    <rect x={xPos + (widthSize*BusinessUnitShare[9]) + (widthSize*BusinessUnitShare[10]) + 2*Hspacing }
    y={yPos - heightSize*CategoryShare[3] - heightSize*CategoryShare[6] - heightSize*CategoryShare[9]-  3*Vspacing}
    width={(widthSize*BusinessUnitShare[11])}
    height={heightSize*CategoryShare[11]}
    style="fill:{LuxFill};stroke:{PotionsScrollsStroke};stroke-width:{StrokeWidth};fill-opacity:{Opacity};stroke-opacity:0.9">>
    <title>{BusinessUnitShare[1]}</title>
    </rect>

    <!--Fifth 12-13 Animals & Transportation-->
    <text x={xPos-185-verticalBarSize} y={yPos + 2 + heightSize*CategoryShare[12]- heightSize*CategoryShare[3] - heightSize*CategoryShare[0]}
          fill="black" font-size={textSizeCategory}>{Type[12]}</text>
    <!--Fifth 12-13 Animals & Transportation CategoryShare-->
    <!-- svelte-ignore a11y-no-static-element-interactions -->
    <!-- svelte-ignore a11y-mouse-events-have-key-events -->
    <rect x={xPos - verticalBarSize}
    y={yPos - heightSize*CategoryShare[3] - heightSize*CategoryShare[6] - heightSize*CategoryShare[9]- heightSize*CategoryShare[12]-  4*Vspacing}
    width={verticalBarWidth}
    height={heightSize*CategoryShare[12]}
    style="fill:{AnimalsTransportStroke};stroke:{AnimalsTransportStroke};stroke-width:{StrokeWidth};
    fill-opacity:{hovered == 'ANIMALS & TRANSPORTATION'? 1.0: categoryShareOpacity};stroke-opacity:0.9"
      on:mouseover={() => startHover('ANIMALS & TRANSPORTATION')}
      on:mouseout={endHover}>
    <title>{CategoryShare[12]}</title>
    </rect>
    {#if hovered=='ANIMALS & TRANSPORTATION'}
      <g transform="translate(700)">
        <Years prType={hovered}/>
      </g>
    {/if}
    <!--Fifth 12-13 Animals & Transportation BusinessUnit-->

    <rect x={xPos}
    y={yPos - heightSize*CategoryShare[3] - heightSize*CategoryShare[6] - heightSize*CategoryShare[9]- heightSize*CategoryShare[12]-  4*Vspacing}
    width={widthSize*(BusinessUnitShare[12]+0.025)}
    height={heightSize*CategoryShare[12]}
    style="fill:{AdvFill};stroke:{AnimalsTransportStroke};stroke-width:{StrokeWidth};fill-opacity:{Opacity};stroke-opacity:0.9">
    <title>{BusinessUnitShare[12]}</title>
    </rect>

    <rect x={xPos  + (widthSize*(BusinessUnitShare[12] + 0.025)) + Hspacing}
    y={yPos - heightSize*CategoryShare[3] - heightSize*CategoryShare[6] - heightSize*CategoryShare[9]- heightSize*CategoryShare[12]-  4*Vspacing}
    width={widthSize*(BusinessUnitShare[13] +0.015)}
    height={heightSize*CategoryShare[13]}
    style="fill:{LuxFill};stroke:{AnimalsTransportStroke};stroke-width:{StrokeWidth};fill-opacity:{Opacity};stroke-opacity:0.9">>
    <title>{BusinessUnitShare[13]}</title>
    </rect>

    <!--Sixth 14-16 Jewelry-->
    <text x={xPos-58-verticalBarSize} y={yPos + 4 -heightSize*CategoryShare[14] - heightSize*CategoryShare[3] - heightSize*CategoryShare[0]}
      fill="black" font-size={textSizeCategory}>{Type[14]}</text>
    <!--Sixth 14-16 Jewelry CategoryShare-->
    <!-- svelte-ignore a11y-no-static-element-interactions -->
    <!-- svelte-ignore a11y-mouse-events-have-key-events -->
    <rect x={xPos - verticalBarSize}
    y={yPos - heightSize*CategoryShare[3] - heightSize*CategoryShare[6] 
      - heightSize*CategoryShare[9]- heightSize*CategoryShare[12] - heightSize*CategoryShare[14] -  5*Vspacing}
    width={verticalBarWidth}
    height={heightSize*CategoryShare[14]}
    style="fill:{JewelryStroke};stroke:{JewelryStroke};stroke-width:{StrokeWidth};
    fill-opacity:{hovered=='JEWELRY'? 1.0: categoryShareOpacity};stroke-opacity:0.9"
      on:mouseover={() => startHover('JEWELRY')}
      on:mouseout={endHover}>
    <title>{CategoryShare[14]}</title>
    </rect>
    {#if hovered=='JEWELRY'}
      <g transform="translate(700)">
        <Years prType={hovered}/>
      </g>
    {/if}
    <!--Sixth 14-16 Jewelry BusinessUnit-->

    <rect x={xPos}
    y={yPos - heightSize*CategoryShare[3] - heightSize*CategoryShare[6] 
      - heightSize*CategoryShare[9]- heightSize*CategoryShare[12] - heightSize*CategoryShare[14] -  5*Vspacing}
    width={widthSize*(BusinessUnitShare[14])}
    height={heightSize*CategoryShare[14]}
    style="fill:{AdvFill};stroke:{JewelryStroke};stroke-width:{StrokeWidth};fill-opacity:{Opacity};stroke-opacity:0.9">
    <title>{BusinessUnitShare[14]}</title>
    </rect>

    <rect x={xPos  + (widthSize*(BusinessUnitShare[14])) + Hspacing}
    y={yPos - heightSize*CategoryShare[3] - heightSize*CategoryShare[6] 
      - heightSize*CategoryShare[9]- heightSize*CategoryShare[12] - heightSize*CategoryShare[14] -  5*Vspacing}
    width={widthSize*(BusinessUnitShare[15])}
    height={heightSize*CategoryShare[15]}
    style="fill:{ComFill};stroke:{JewelryStroke};stroke-width:{StrokeWidth};fill-opacity:{Opacity};stroke-opacity:0.9">>
    <title>{BusinessUnitShare[15]}</title>
    </rect>
      
    <rect x={xPos  + (widthSize*BusinessUnitShare[14]) + (widthSize*BusinessUnitShare[15]) + 2*Hspacing }
    y={yPos - heightSize*CategoryShare[3] - heightSize*CategoryShare[6] 
    - heightSize*CategoryShare[9]- heightSize*CategoryShare[12] - heightSize*CategoryShare[14] -  5*Vspacing}
    width={(widthSize*BusinessUnitShare[16])}
    height={heightSize*CategoryShare[16]}
    style="fill:{LuxFill};stroke:{JewelryStroke};stroke-width:{StrokeWidth};fill-opacity:{Opacity};stroke-opacity:0.9">>
    <title>{BusinessUnitShare[16]}</title>
    </rect>

    <!--Seventh 17-19 Summoning Device-->
    <text x={xPos-133-verticalBarSize} y={yPos + 2 - heightSize*CategoryShare[0]- heightSize*CategoryShare[3] - heightSize*CategoryShare[6]}
      fill="black" font-size={textSizeCategory}>{Type[17]}</text>
      <!--Seventh 17-19 Summoning Device CategoryShare-->
      <!-- svelte-ignore a11y-no-static-element-interactions -->
      <!-- svelte-ignore a11y-mouse-events-have-key-events -->
      <rect x={xPos - verticalBarSize}
    y={yPos - heightSize*CategoryShare[3] - heightSize*CategoryShare[6] 
      - heightSize*CategoryShare[9]- heightSize*CategoryShare[12] - heightSize*CategoryShare[14] - heightSize*CategoryShare[17] -  6*Vspacing}
    width={verticalBarWidth}
    height={heightSize*CategoryShare[17]}
    style="fill:{SummoningDeviceStroke};stroke:{SummoningDeviceStroke};stroke-width:{StrokeWidth};
    fill-opacity:{hovered=='SUMMONING DEVICE'? 1.0: categoryShareOpacity};stroke-opacity:0.9"
      on:mouseover={() => startHover('SUMMONING DEVICE')}
      on:mouseout={endHover}>
    <title>{CategoryShare[17]}</title>
    </rect>
    {#if hovered=='SUMMONING DEVICE'}
      <g transform="translate(700)">
        <Years prType={hovered}/>
      </g>
    {/if}
      <!--Seventh 17-19 Summoning Device BusinessUnit-->
    <rect x={xPos}
    y={yPos - heightSize*CategoryShare[3] - heightSize*CategoryShare[6] 
      - heightSize*CategoryShare[9]- heightSize*CategoryShare[12] - heightSize*CategoryShare[14] - heightSize*CategoryShare[17] -  6*Vspacing}
    width={widthSize*(BusinessUnitShare[17])}
    height={heightSize*CategoryShare[17]}
    style="fill:{AdvFill};stroke:{SummoningDeviceStroke};stroke-width:{StrokeWidth};fill-opacity:{Opacity};stroke-opacity:0.9">
    <title>{BusinessUnitShare[17]}</title>
    </rect>

    <rect x={xPos  + (widthSize*(BusinessUnitShare[17])) + Hspacing}
    y={yPos - heightSize*CategoryShare[3] - heightSize*CategoryShare[6] 
      - heightSize*CategoryShare[9]- heightSize*CategoryShare[12] - heightSize*CategoryShare[14] - heightSize*CategoryShare[17] -  6*Vspacing}
    width={widthSize*(BusinessUnitShare[18])}
    height={heightSize*CategoryShare[18]}
    style="fill:{ComFill};stroke:{SummoningDeviceStroke};stroke-width:{StrokeWidth};fill-opacity:{Opacity};stroke-opacity:0.9">>
    <title>{BusinessUnitShare[18]}</title>
    </rect>
      
    <rect x={xPos  + (widthSize*BusinessUnitShare[17]) + (widthSize*BusinessUnitShare[18]) + 2*Hspacing }
    y={yPos - heightSize*CategoryShare[3] - heightSize*CategoryShare[6] 
      - heightSize*CategoryShare[9]- heightSize*CategoryShare[12] - heightSize*CategoryShare[14] - heightSize*CategoryShare[17] -  6*Vspacing}
    width={(widthSize*BusinessUnitShare[19])}
    height={heightSize*CategoryShare[19]}
    style="fill:{LuxFill};stroke:{SummoningDeviceStroke};stroke-width:{StrokeWidth};fill-opacity:{Opacity};stroke-opacity:0.9">>
    <title>{BusinessUnitShare[19]}</title>
    </rect>

    <!--Seventh 20-21 Musical Instrument-->
    <text x={xPos-142-verticalBarSize} y={yPos - 17 -heightSize*CategoryShare[3] - heightSize*CategoryShare[6] - 
      heightSize*CategoryShare[0]}
      fill="black" font-size={textSizeCategory}>{Type[20]}</text>

    <!--Seventh 20-21 Musical Instrument CategoryShare-->
    <!-- svelte-ignore a11y-mouse-events-have-key-events -->
    <!-- svelte-ignore a11y-no-static-element-interactions -->
    <rect x={xPos - verticalBarSize}
    y={yPos - heightSize*CategoryShare[3] - heightSize*CategoryShare[6] 
      - heightSize*CategoryShare[9]- heightSize*CategoryShare[12] - heightSize*CategoryShare[14] - heightSize*CategoryShare[17]
      -heightSize*CategoryShare[20] -  7*Vspacing}
    width={verticalBarWidth}
    height={heightSize*CategoryShare[20]}
    style="fill:{MusicalInstrumentStroke};stroke:{MusicalInstrumentStroke};stroke-width:{StrokeWidth};
    fill-opacity:{hovered=='MUSICAL INSTRUMENT'? 1.0: categoryShareOpacity};stroke-opacity:0.9"
      on:mouseover={() => startHover('MUSICAL INSTRUMENT')}
      on:mouseout={endHover}>
    <title>{CategoryShare[20]}</title>
    </rect>
    
    {#if hovered=='MUSICAL INSTRUMENT'}
      <g transform="translate(700)">
        <Years prType='MUSICAL INSTRUMENT'/>
      </g>
    {/if}

    <!--Seventh 20-21 Musical Instrument BusinessUnit-->
    <rect x={xPos}
    y={yPos - heightSize*CategoryShare[3] - heightSize*CategoryShare[6] 
      - heightSize*CategoryShare[9]- heightSize*CategoryShare[12] - heightSize*CategoryShare[14] - heightSize*CategoryShare[17]
      -heightSize*CategoryShare[20] -  7*Vspacing}
    width={widthSize*(BusinessUnitShare[20]+0.015 )}
    height={heightSize*CategoryShare[20]}
    style="fill:{AdvFill};stroke:{MusicalInstrumentStroke};stroke-width:{StrokeWidth};fill-opacity:{Opacity};stroke-opacity:0.9">
    <title>{BusinessUnitShare[20]}</title>
    </rect>

    <rect x={xPos  + (widthSize*(BusinessUnitShare[20]+0.015)) + Hspacing}
    y={yPos - heightSize*CategoryShare[3] - heightSize*CategoryShare[6] 
      - heightSize*CategoryShare[9]- heightSize*CategoryShare[12] - heightSize*CategoryShare[14] - heightSize*CategoryShare[17]
      -heightSize*CategoryShare[20] -  7*Vspacing}
    width={widthSize*(BusinessUnitShare[21]+0.025)}
    height={heightSize*CategoryShare[21]}
    style="fill:{LuxFill};stroke:{MusicalInstrumentStroke};stroke-width:{StrokeWidth};fill-opacity:{Opacity};stroke-opacity:0.9">>
    <title>{BusinessUnitShare[21]}</title>
    </rect>

    <!--Shopping Bag Handle-->
    <path d="M 370 140
            C 370 140, 430 -105, 500 140"
            stroke="black" fill="transparent"stroke-width="3" fill-opacity="0.5"/>
    <path d="M 365 140
            C 365 140, 430 -120, 505 140"
            stroke="black" fill="transparent"stroke-width="4" fill-opacity="0.5"/>

    <path d="M 297 140 l 276 0"
            stroke="black" fill="transparent"stroke-width="3" fill-opacity="0.5"/>
    <path d="M 297 521 l 276 0"
            stroke="black" fill="transparent"stroke-width="3" fill-opacity="0.5"/>



    <!--Legends BusinessUnit-->
    <text x={xPos - 5} y={yPos + 150} fill="black" font-size={textSizeCategory}>ADVENTURING</text>
    <rect 
      x={xPos - legendBox - Hspacing}
      y={yPos + 145 - legendBox + Vspacing}
      width={legendBox}
      height={legendBox}
      style="fill:{AdvFill};fill-opacity:{Opacity};stroke:black;stroke-width:2:stroke-opacity:0.9">
      <title></title>
    </rect>

    <text x={xPos + 130 -5} y={yPos + 150} fill="black" font-size={textSizeCategory}>COMMISSIONS</text>
    <rect 
      x={xPos + 130 - legendBox - Hspacing}
      y={yPos + 145 - legendBox + Vspacing}
      width={legendBox}
      height={legendBox}
      style="fill:{ComFill};fill-opacity:{Opacity};stroke:black;stroke-width:2:stroke-opacity:0.9">
      <title></title>
    </rect>

    <text x={xPos + 260 -5} y={yPos + 150} fill="black" font-size={textSizeCategory}>LUXURY SPECIALTIES</text>
    <rect 
      x={xPos +260 - legendBox - Hspacing}
      y={yPos + 145 - legendBox + Vspacing}
      width={legendBox}
      height={legendBox}
      style="fill:{LuxFill};fill-opacity:{Opacity};stroke:black;stroke-width:2:stroke-opacity:0.9">
      <title></title>
    </rect>

  </g>
</svg>