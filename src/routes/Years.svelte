<script>
// @ts-nocheck
 
    import { scaleLinear } from 'd3-scale';

    import data from './circleDataList.json';
    // let prType = 'ADVENTURING EQUIPMENT';
    // let prType = 'ANIMALS & TRANSPORTATION';
    // let prType = 'ARMS & ARMOUR';
    // let prType = 'JEWELRY';
    // let prType = 'MUSICAL INSTRUMENT';
    // let prType = 'POTIONS & SCROLLS';
    // let prType = 'SUMMONING DEVICE';
    // let prType = 'TOOLS & KITS';
    export let prType;

    let parsedData = data.map((d) => {
        return {
            type: d['type'],
            y19: d['2019'],
            y20: d['2020'],
            y21: d['2021'],
            y22: d['2022'],
            y23: d['2023'],
            extentMin: d['minExtent'],
            extentMax: d['maxExtent'],
            sum: d['sum']
        }
    });
    let usedType;
    parsedData.forEach(d => {
        if (d.type == prType) {
            usedType = d;
        }
    });
    // console.log(usedType)

    const width = 600;
    const height = 600;
    const margin = { top: 5, right: 5, bottom: 5, left: 5 };

    let scaleData = scaleLinear().domain([usedType.extentMin, usedType.extentMax]).range([20, height/3-20]);
    function transformX(m, d) {
        return Math.sin((m+1)*(Math.PI/6))*scaleData(d[m]);
    }
    function transformY(m, d) {
        return Math.cos((m+1)*(Math.PI/6))*scaleData(d[m]);
    }

</script>

<style>
    text{
        font-family:'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        fill:black;
        stroke:black;
    }
    svg {
        border: 1px;
        border-style: solid;
    }
    .web {
        stroke: black;
        stroke-width: 2;
        stroke-dasharray: 15,10;
        stroke-opacity: 0.1;
    }
    .obrub {
        fill: none;
        stroke: black;
        stroke-width: 2;
        opacity: 0.5;
    }
    .monthName {
        fill: black;
        font-size: 140%;
    }
    #path19 {
        fill: none;
        stroke: blue;
        stroke-width: 2;
        stroke-opacity: 0.5;
    }
    #path20 {
        fill: none;
        stroke: red;
        stroke-width: 2;
        stroke-opacity: 0.5;
    }
    #path21 {
        fill: none;
        stroke: green;
        stroke-width: 2;
        stroke-opacity: 0.5;
    }
    #path22 {
        fill: none;
        stroke: purple;
        stroke-width: 2;
        stroke-opacity: 0.5;
    }
    #path23 {
        fill: none;
        stroke: orange;
        stroke-width: 2;
        stroke-opacity: 0.5;
    }
</style>

<svg {width} {height}>
    <g transform="translate({width/2}, {height/2})">
        <g transform="translate(0,-20)">
            {#each [0,1,2,3,4,5] as offset}
                <line class='web' x1=0 y1={-height/3} x2=0 y2={height/3} transform="rotate({offset*30})"/>
            {/each}
            <circle class='obrub' r={height/3} cx=0 cy=0 />

            <text class='monthName' x=-20 y={-height/3-5}>Dec</text>
            <text class='monthName' x=-20 y={-height/3-5} transform="rotate(30)">Jan</text>
            <text class='monthName' x=-20 y={-height/3-5} transform="rotate(60)">Feb</text>
            <text class='monthName' x=-20 y={-height/3-5} transform="rotate(90)">Mar</text>
            <text class='monthName' x=-10 y={height/3+25} transform="rotate(-60)">Apr</text>
            <text class='monthName' x=-10 y={height/3+25} transform="rotate(-30)">May</text>
            <text class='monthName' x=-10 y={height/3+25}>Jun</text>
            <text class='monthName' x=-10 y={height/3+25} transform="rotate(30)">Jul</text>
            <text class='monthName' x=-10 y={height/3+25} transform="rotate(60)">Aug</text>
            <text class='monthName' x=-20 y={-height/3-5} transform="rotate(-90)">Sep</text>
            <text class='monthName' x=-20 y={-height/3-5} transform="rotate(-60)">Oct</text>
            <text class='monthName' x=-20 y={-height/3-5} transform="rotate(-30)">Nov</text>

            <path id='path19' d="M {transformX(11, usedType.y19)},{-transformY(11, usedType.y19)} 
                L {transformX(0, usedType.y19)},{-transformY(0, usedType.y19)} 
                L {transformX(1, usedType.y19)},{-transformY(1, usedType.y19)}
                L {transformX(2, usedType.y19)},{-transformY(2, usedType.y19)}
                L {transformX(3, usedType.y19)},{-transformY(3, usedType.y19)}
                L {transformX(4, usedType.y19)},{-transformY(4, usedType.y19)}
                L {transformX(5, usedType.y19)},{-transformY(5, usedType.y19)}
                L {transformX(6, usedType.y19)},{-transformY(6, usedType.y19)}
                L {transformX(7, usedType.y19)},{-transformY(7, usedType.y19)}
                L {transformX(8, usedType.y19)},{-transformY(8, usedType.y19)}
                L {transformX(9, usedType.y19)},{-transformY(9, usedType.y19)}
                L {transformX(10, usedType.y19)},{-transformY(10, usedType.y19)} Z" />
            <circle r=5 cx={width/2-100} cy={-height/2+50} fill='blue' opacity=0.5/>
            <text x={width/2-90} y={-height/2+55} font-size=20>2019</text>

            <path id='path20' d="M {transformX(11, usedType.y20)},{-transformY(11, usedType.y20)} 
                L {transformX(0, usedType.y20)},{-transformY(0, usedType.y20)} 
                L {transformX(1, usedType.y20)},{-transformY(1, usedType.y20)}
                L {transformX(2, usedType.y20)},{-transformY(2, usedType.y20)}
                L {transformX(3, usedType.y20)},{-transformY(3, usedType.y20)}
                L {transformX(4, usedType.y20)},{-transformY(4, usedType.y20)}
                L {transformX(5, usedType.y20)},{-transformY(5, usedType.y20)}
                L {transformX(6, usedType.y20)},{-transformY(6, usedType.y20)}
                L {transformX(7, usedType.y20)},{-transformY(7, usedType.y20)}
                L {transformX(8, usedType.y20)},{-transformY(8, usedType.y20)}
                L {transformX(9, usedType.y20)},{-transformY(9, usedType.y20)}
                L {transformX(10, usedType.y20)},{-transformY(10, usedType.y20)} Z" />
            <circle r=5 cx={width/2-100} cy={-height/2+75} fill='red' opacity=0.5/>
            <text x={width/2-90} y={-height/2+80} font-size=20>2020</text>

            <path id='path21' d="M {transformX(11, usedType.y21)},{-transformY(11, usedType.y21)} 
                L {transformX(0, usedType.y21)},{-transformY(0, usedType.y21)} 
                L {transformX(1, usedType.y21)},{-transformY(1, usedType.y21)}
                L {transformX(2, usedType.y21)},{-transformY(2, usedType.y21)}
                L {transformX(3, usedType.y21)},{-transformY(3, usedType.y21)}
                L {transformX(4, usedType.y21)},{-transformY(4, usedType.y21)}
                L {transformX(5, usedType.y21)},{-transformY(5, usedType.y21)}
                L {transformX(6, usedType.y21)},{-transformY(6, usedType.y21)}
                L {transformX(7, usedType.y21)},{-transformY(7, usedType.y21)}
                L {transformX(8, usedType.y21)},{-transformY(8, usedType.y21)}
                L {transformX(9, usedType.y21)},{-transformY(9, usedType.y21)}
                L {transformX(10, usedType.y21)},{-transformY(10, usedType.y21)} Z" />
            <circle r=5 cx={width/2-100} cy={-height/2+100} fill = 'green' opacity=0.5/>
            <text x={width/2-90} y={-height/2+105} font-size=20>2021</text>

            <path id='path22' d="M {transformX(11, usedType.y22)},{-transformY(11, usedType.y22)} 
                L {transformX(0, usedType.y22)},{-transformY(0, usedType.y22)} 
                L {transformX(1, usedType.y22)},{-transformY(1, usedType.y22)}
                L {transformX(2, usedType.y22)},{-transformY(2, usedType.y22)}
                L {transformX(3, usedType.y22)},{-transformY(3, usedType.y22)}
                L {transformX(4, usedType.y22)},{-transformY(4, usedType.y22)}
                L {transformX(5, usedType.y22)},{-transformY(5, usedType.y22)}
                L {transformX(6, usedType.y22)},{-transformY(6, usedType.y22)}
                L {transformX(7, usedType.y22)},{-transformY(7, usedType.y22)}
                L {transformX(8, usedType.y22)},{-transformY(8, usedType.y22)}
                L {transformX(9, usedType.y22)},{-transformY(9, usedType.y22)}
                L {transformX(10, usedType.y22)},{-transformY(10, usedType.y22)} Z" />
            <circle r=5 cx={width/2-100} cy={-height/2+125} fill = 'purple' opacity=0.5/>
            <text x={width/2-90} y={-height/2+130} font-size=20>2022</text>

            <path id='path23' d="M {transformX(11, usedType.y23)},{-transformY(11, usedType.y23)} 
                L {transformX(0, usedType.y23)},{-transformY(0, usedType.y23)} 
                L {transformX(1, usedType.y23)},{-transformY(1, usedType.y23)}
                L {transformX(2, usedType.y23)},{-transformY(2, usedType.y23)}
                L {transformX(3, usedType.y23)},{-transformY(3, usedType.y23)}
                L {transformX(4, usedType.y23)},{-transformY(4, usedType.y23)}
                L {transformX(5, usedType.y23)},{-transformY(5, usedType.y23)}
                L {transformX(6, usedType.y23)},{-transformY(6, usedType.y23)}
                L {transformX(7, usedType.y23)},{-transformY(7, usedType.y23)}
                L {transformX(8, usedType.y23)},{-transformY(8, usedType.y23)}
                L {transformX(9, usedType.y23)},{-transformY(9, usedType.y23)}
                L {transformX(10, usedType.y23)},{-transformY(10, usedType.y23)} Z" />
            <circle r=5 cx={width/2-100} cy={-height/2+150} fill = 'orange' opacity=0.5/>
            <text x={width/2-90} y={-height/2+155} font-size=20>2023</text>
        </g>

        <text x={-width/4-30} y={height/2-50} font-size=20> NUMBER OF ORDERS THROUGH EACH YEAR</text>
        <text x={-width/4} y={height/2-25} font-size=15 font-style="italic"> Total number of orders for this category: {usedType.sum}</text>


        <!-- {#each [11,0,1,2,3,4,5,6,7,8,9,10] as m}
            <circle r=3 cx={transformX(m, usedType.y19)} cy={-transformY(m, usedType.y19)} fill='red' />
        {/each} -->
        

        <!-- {#each [11,0,1,2,3,4,5,6,7,8,9,10] as m}
            <circle r=3 cx=0 cy={-scaleData(usedType.y20[m])} transform="rotate({(m+1)*30})" fill='blue'/>
        {/each}
        {#each [11,0,1,2,3,4,5,6,7,8,9,10] as m}
            <circle r=3 cx=0 cy={-scaleData(usedType.y21[m])} transform="rotate({(m+1)*30})" fill='green'/>
        {/each}
        {#each [11,0,1,2,3,4,5,6,7,8,9,10] as m}
            <circle r=3 cx=0 cy={-scaleData(usedType.y22[m])} transform="rotate({(m+1)*30})" fill='orange'/>
        {/each}
        {#each [11,0,1,2,3,4,5,6,7,8,9,10] as m}
            <circle r=3 cx=0 cy={-scaleData(usedType.y23[m])} transform="rotate({(m+1)*30})" fill='purple'/>
        {/each} -->
    </g>
</svg>
    