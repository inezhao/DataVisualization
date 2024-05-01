<!-- page.svelte -->

<script>
    import shoppingData from './shopping.json';
    const BusinessUnitShare = shoppingData.BusinessUnitShare;
    const CategoryShare = shoppingData.CategoryShare;
    const Type = shoppingData.Type;
    const Quantities = shoppingData.Quantities;
    const BusinessUnit = shoppingData.BusinessUnit;

    const widthSize = 200;
    const heightSize = 150;
    const xPos = 150;
    const yPos = 200;
    //export let data2 = [100, 200, 150 ,250];
    //export let total = [150, 300, 300, 280];
</script>
  
<h2>Title</h2>
<style>
  rect{
    fill: blue;
  }
</style>

<svg width=800 height=400>
<!--First 0-2 Arms & Armour-->
<text x={xPos-120} y="230" fill="black" font-size="8">{Type[0]}</text>
  <rect x={xPos}
  y={200}
  width={(widthSize*BusinessUnitShare[0])}
  height={heightSize*CategoryShare[0]}
  style="fill:cyan;stroke:pink;stroke-width:2;fill-opacity:0.9;stroke-opacity:0.9">
  <title>{BusinessUnitShare[0]}</title>
  </rect>

  <rect x={xPos  + (widthSize*BusinessUnitShare[0]) + 5 }
  y={200}
  width={(widthSize*BusinessUnitShare[1])}
  height={heightSize*CategoryShare[1]}
  style="fill:cyan;stroke:pink;stroke-width:2;fill-opacity:0.3;stroke-opacity:0.9">>
  <title>{BusinessUnitShare[1]}</title>
  </rect>
    
  <rect x={xPos  + (widthSize*BusinessUnitShare[0]) + (widthSize*BusinessUnitShare[1]) + 10 }
  y={200}
  width={(widthSize*BusinessUnitShare[2])}
  height={heightSize*CategoryShare[2]}
  style="fill:cyan;stroke:pink;stroke-width:2;fill-opacity:0.1;stroke-opacity:0.9">>
  <title>{BusinessUnitShare[2]}</title>
  </rect>

<!--Second 3-5 Adventuring Equipment-->
<text x={xPos-120} y={230 - heightSize*CategoryShare[3] - 5} fill="black" font-size="8">{Type[3]}</text>
<rect x={xPos}
y={200 - heightSize*CategoryShare[3] - 5}
width={(widthSize*BusinessUnitShare[3])}
height={heightSize*CategoryShare[3]}
style="fill:magenta;stroke:pink;stroke-width:2;fill-opacity:0.9;stroke-opacity:0.9">
<title>{BusinessUnitShare[3]}</title>
</rect>

<rect x={xPos  + (widthSize*BusinessUnitShare[3]) + 5 }
y={200 - heightSize*CategoryShare[4] - 5}
width={(widthSize*BusinessUnitShare[4])}
height={heightSize*CategoryShare[4]}
style="fill:magenta;stroke:pink;stroke-width:2;fill-opacity:0.3;stroke-opacity:0.9">>
<title>{BusinessUnitShare[4]}</title>
</rect>
  
<rect x={xPos + (widthSize*BusinessUnitShare[3]) + (widthSize*BusinessUnitShare[4]) + 10}
y={200 - heightSize*CategoryShare[5] - 5}
width={(widthSize*BusinessUnitShare[5])}
height={heightSize*CategoryShare[5]}
style="fill:magenta;stroke:pink;stroke-width:2;fill-opacity:0.1;stroke-opacity:0.9">>
<title>{BusinessUnitShare[5]}</title>
</rect>

<!--Third 6-8 Tools & Kits-->
<text x={xPos-120} y={200 - heightSize*CategoryShare[3] - heightSize*CategoryShare[6]} fill="black" font-size="8">{Type[6]}</text>
<rect x={xPos}
y={200 - heightSize*CategoryShare[3] - heightSize*CategoryShare[6] - 10}
width={(widthSize*BusinessUnitShare[6])}
height={heightSize*CategoryShare[6]}
style="fill:darkblue;stroke:pink;stroke-width:2;fill-opacity:0.9;stroke-opacity:0.9">
<title>{BusinessUnitShare[6]}</title>
</rect>

<rect x={xPos  + (widthSize*BusinessUnitShare[6]) + 5 }
y={200 - heightSize*CategoryShare[3] - heightSize*CategoryShare[7] - 10}
width={(widthSize*BusinessUnitShare[7])}
height={heightSize*CategoryShare[7]}
style="fill:darkblue;stroke:pink;stroke-width:2;fill-opacity:0.3;stroke-opacity:0.9">>
<title>{BusinessUnitShare[7]}</title>
</rect>
  
<rect x={xPos + (widthSize*BusinessUnitShare[6]) + (widthSize*BusinessUnitShare[7]) + 10 }
y={200 - heightSize*CategoryShare[3] - heightSize*CategoryShare[8] - 10}
width={(widthSize*BusinessUnitShare[8])}
height={heightSize*CategoryShare[8]}
style="fill:darkblue;stroke:pink;stroke-width:2;fill-opacity:0.1;stroke-opacity:0.9">>
<title>{BusinessUnitShare[8]}</title>
</rect>

<!--Fourth 9-11 Potions & Scrolls-->
<text x={xPos-120} y={200 - heightSize*CategoryShare[3] - heightSize*CategoryShare[6] - heightSize*CategoryShare[9] -5}
      fill="black" font-size="8">{Type[9]}</text>
<rect x={xPos}
y={200 - heightSize*CategoryShare[3] - heightSize*CategoryShare[6] - heightSize*CategoryShare[9]- 15}
width={(widthSize*BusinessUnitShare[9])}
height={heightSize*CategoryShare[9]}
style="fill:blue;stroke:pink;stroke-width:2;fill-opacity:0.9;stroke-opacity:0.9">
<title>{BusinessUnitShare[9]}</title>
</rect>

<rect x={xPos  + (widthSize*BusinessUnitShare[9]) + 5 }
y={200 - heightSize*CategoryShare[3] - heightSize*CategoryShare[6] - heightSize*CategoryShare[9]- 15}
width={(widthSize*BusinessUnitShare[10])}
height={heightSize*CategoryShare[10]}
style="fill:blue;stroke:pink;stroke-width:2;fill-opacity:0.3;stroke-opacity:0.9">>
<title>{BusinessUnitShare[10]}</title>
</rect>
  
<rect x={xPos + (widthSize*BusinessUnitShare[9]) + (widthSize*BusinessUnitShare[10]) + 10 }
y={200 - heightSize*CategoryShare[3] - heightSize*CategoryShare[6] - heightSize*CategoryShare[9]- 15}
width={(widthSize*BusinessUnitShare[11])}
height={heightSize*CategoryShare[11]}
style="fill:blue;stroke:pink;stroke-width:2;fill-opacity:0.1;stroke-opacity:0.9">>
<title>{BusinessUnitShare[1]}</title>
</rect>

<!--Fifth 12-13 Animals & Transportation-->
<text x={xPos-120} y={200 - heightSize*CategoryShare[3] - heightSize*CategoryShare[6] - 
      heightSize*CategoryShare[9] -heightSize*CategoryShare[12] - 12}
      fill="black" font-size="8">{Type[12]}</text>
<rect x={xPos}
y={200 - heightSize*CategoryShare[3] - heightSize*CategoryShare[6] - heightSize*CategoryShare[9]- heightSize*CategoryShare[12]-20}
width={widthSize*(BusinessUnitShare[12]+0.025)}
height={heightSize*CategoryShare[12]}
style="fill:green;stroke:pink;stroke-width:2;fill-opacity:0.9;stroke-opacity:0.9">
<title>{BusinessUnitShare[12]}</title>
</rect>

<rect x={xPos  + (widthSize*(BusinessUnitShare[12] + 0.025)) + 5}
y={200 - heightSize*CategoryShare[3] - heightSize*CategoryShare[6] - heightSize*CategoryShare[9]- heightSize*CategoryShare[12]-20}
width={widthSize*(BusinessUnitShare[13])}
height={heightSize*CategoryShare[13]}
style="fill:green;stroke:pink;stroke-width:2;fill-opacity:0.3;stroke-opacity:0.9">>
<title>{BusinessUnitShare[13]}</title>
</rect>

<!--Sixth 14-16 Jewelry-->
<text x={xPos-120} y={200 - heightSize*CategoryShare[3] - heightSize*CategoryShare[6] - 
  heightSize*CategoryShare[9] -heightSize*CategoryShare[12] - heightSize*CategoryShare[14] - 20}
  fill="black" font-size="8">{Type[14]}</text>
<rect x={xPos}
y={200 - heightSize*CategoryShare[3] - heightSize*CategoryShare[6] 
  - heightSize*CategoryShare[9]- heightSize*CategoryShare[12] - heightSize*CategoryShare[14] - 25}
width={widthSize*(BusinessUnitShare[14])}
height={heightSize*CategoryShare[14]}
style="fill:yellow;stroke:pink;stroke-width:2;fill-opacity:0.9;stroke-opacity:0.9">
<title>{BusinessUnitShare[14]}</title>
</rect>

<rect x={xPos  + (widthSize*(BusinessUnitShare[14])) + 5}
y={200 - heightSize*CategoryShare[3] - heightSize*CategoryShare[6] 
  - heightSize*CategoryShare[9]- heightSize*CategoryShare[12] - heightSize*CategoryShare[14] - 25}
width={widthSize*(BusinessUnitShare[15])}
height={heightSize*CategoryShare[15]}
style="fill:yellow;stroke:pink;stroke-width:2;fill-opacity:0.3;stroke-opacity:0.9">>
<title>{BusinessUnitShare[15]}</title>
</rect>
  
<rect x={xPos  + (widthSize*BusinessUnitShare[14]) + (widthSize*BusinessUnitShare[15]) + 10 }
y={200 - heightSize*CategoryShare[3] - heightSize*CategoryShare[6] 
- heightSize*CategoryShare[9]- heightSize*CategoryShare[12] - heightSize*CategoryShare[14] - 25}
width={(widthSize*BusinessUnitShare[16])}
height={heightSize*CategoryShare[16]}
style="fill:yellow;stroke:pink;stroke-width:2;fill-opacity:0.1;stroke-opacity:0.9">>
<title>{BusinessUnitShare[16]}</title>
</rect>

<!--Seventh 17-19 Summoning Device-->
<text x={xPos-120} y={200 - heightSize*CategoryShare[3] - heightSize*CategoryShare[6] - 
  heightSize*CategoryShare[9] -heightSize*CategoryShare[12] - heightSize*CategoryShare[14] - heightSize*CategoryShare[17] - 25}
  fill="black" font-size="8">{Type[17]}</text>
<rect x={xPos}
y={200 - heightSize*CategoryShare[3] - heightSize*CategoryShare[6] 
  - heightSize*CategoryShare[9]- heightSize*CategoryShare[12] - heightSize*CategoryShare[14] - heightSize*CategoryShare[17] - 30}
width={widthSize*(BusinessUnitShare[17])}
height={100*CategoryShare[17]}
style="fill:orange;stroke:pink;stroke-width:2;fill-opacity:0.9;stroke-opacity:0.9">
<title>{BusinessUnitShare[17]}</title>
</rect>

<rect x={xPos  + (widthSize*(BusinessUnitShare[17])) + 5}
y={200 - heightSize*CategoryShare[3] - heightSize*CategoryShare[6] 
  - heightSize*CategoryShare[9]- heightSize*CategoryShare[12] - heightSize*CategoryShare[14] - heightSize*CategoryShare[17] - 30}
width={widthSize*(BusinessUnitShare[18])}
height={100*CategoryShare[18]}
style="fill:orange;stroke:pink;stroke-width:2;fill-opacity:0.3;stroke-opacity:0.9">>
<title>{BusinessUnitShare[18]}</title>
</rect>
  
<rect x={xPos  + (widthSize*BusinessUnitShare[17]) + (widthSize*BusinessUnitShare[18]) + 10 }
y={200 - heightSize*CategoryShare[3] - heightSize*CategoryShare[6] 
  - heightSize*CategoryShare[9]- heightSize*CategoryShare[12] - heightSize*CategoryShare[14] - heightSize*CategoryShare[17] - 30}
width={(widthSize*BusinessUnitShare[19])}
height={heightSize*CategoryShare[19]}
style="fill:orange;stroke:pink;stroke-width:2;fill-opacity:0.1;stroke-opacity:0.9">>
<title>{BusinessUnitShare[19]}</title>
</rect>

<!--Seventh 20-21 Musical Instrument-->
<text x={xPos-120} y={200 - heightSize*CategoryShare[3] - heightSize*CategoryShare[6] - 
  heightSize*CategoryShare[9] -heightSize*CategoryShare[12] - heightSize*CategoryShare[14] - heightSize*CategoryShare[17] - heightSize*CategoryShare[20] -30}
  fill="black" font-size="8">{Type[20]}</text>
<rect x={xPos}
y={200 - heightSize*CategoryShare[3] - heightSize*CategoryShare[6] 
  - heightSize*CategoryShare[9]- heightSize*CategoryShare[12] - heightSize*CategoryShare[14] - heightSize*CategoryShare[17]
  -heightSize*CategoryShare[20] - 35}
width={widthSize*(BusinessUnitShare[20])}
height={100*CategoryShare[20]}
style="fill:red;stroke:pink;stroke-width:2;fill-opacity:0.9;stroke-opacity:0.9">
<title>{BusinessUnitShare[20]}</title>
</rect>

<rect x={xPos  + (widthSize*(BusinessUnitShare[20])) + 5}
y={200 - heightSize*CategoryShare[3] - heightSize*CategoryShare[6] 
  - heightSize*CategoryShare[9]- heightSize*CategoryShare[12] - heightSize*CategoryShare[14] - heightSize*CategoryShare[17]
  -heightSize*CategoryShare[20] - 35}
width={widthSize*(BusinessUnitShare[21]+0.025)}
height={heightSize*CategoryShare[21]}
style="fill:red;stroke:pink;stroke-width:2;fill-opacity:0.3;stroke-opacity:0.9">>
<title>{BusinessUnitShare[21]}</title>
</rect>

<path d="M 200 70 Q 255 -30 310 70" stroke="black" fill="transparent"/>
<path d="M 200 70 Q 255 -40 310 70" stroke="black" fill="transparent"/>

</svg>