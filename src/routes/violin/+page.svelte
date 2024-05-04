<script>
// @ts-nocheck

  import { onMount } from 'svelte';
  import * as d3 from 'd3';
   
  let data_orig = [
    {BusinessUnit: 'ADVENTURING', Type: 'ADVENTURING EQUIPMENT', averagePrice: 490.7693123341185, averageDeliveryTime: 10.52170589418628 }, 
		{BusinessUnit: 'ADVENTURING',Type: 'ANIMALS & TRANSPORTATION', averagePrice: 537.232760326804, averageDeliveryTime: 9.712276717750939},
		{BusinessUnit: 'ADVENTURING',Type: 'ARMS & ARMOUR', averagePrice: 488.8529626971006, averageDeliveryTime: 10.359471182293708},
		{BusinessUnit: 'ADVENTURING',Type: 'JEWELRY', averagePrice: 514.0333582153216, averageDeliveryTime: 10.610753284422454},
		{BusinessUnit: 'ADVENTURING',Type: 'MUSICAL INSTRUMENT', averagePrice: 497.1466316793893, averageDeliveryTime: 10.064980916030533},
		{BusinessUnit: 'ADVENTURING',Type: 'POTIONS & SCROLLS', averagePrice: 467.2380406103017, averageDeliveryTime: 10.587705776069749},
		{BusinessUnit: 'ADVENTURING',Type: 'SUMMONING DEVICE', averagePrice: 803.1830837930129, averageDeliveryTime: 8.917783031258208},
		{BusinessUnit: 'ADVENTURING',Type: 'TOOLS & KITS', averagePrice: 492.7048527789344, averageDeliveryTime: 9.733143306045529},
		{BusinessUnit: 'COMMISSIONS',Type: 'ADVENTURING EQUIPMENT', averagePrice: 545.4023722193584, averageDeliveryTime: 11.220260517863515},
		{BusinessUnit: 'COMMISSIONS',Type: 'ARMS & ARMOUR', averagePrice: 500.97533123076863, averageDeliveryTime: 10.94976893556702},
		{BusinessUnit: 'COMMISSIONS',Type: 'JEWELRY', averagePrice: 483.9162174416847, averageDeliveryTime: 9.889969267973198},
		{BusinessUnit: 'COMMISSIONS',Type: 'POTIONS & SCROLLS', averagePrice: 391.6539010657551, averageDeliveryTime: 10.734717474361553},
		{BusinessUnit: 'COMMISSIONS',Type: 'SUMMONING DEVICE', averagePrice: 559.5603448275862, averageDeliveryTime: 10.375034046957564},
		{BusinessUnit: 'COMMISSIONS',Type: 'TOOLS & KITS', averagePrice: 364.8769153479025, averageDeliveryTime: 12.106003516704346},
		{BusinessUnit: 'LUXURY SPECIALTIES',Type: 'ADVENTURING EQUIPMENT', averagePrice: 517.7875210040519, averageDeliveryTime: 10.726117732598077},
		{BusinessUnit: 'LUXURY SPECIALTIES',Type: 'ANIMALS & TRANSPORTATION', averagePrice: 468.20614454919024, averageDeliveryTime: 9.788993634678913},
		{BusinessUnit: 'LUXURY SPECIALTIES',Type: 'ARMS & ARMOUR', averagePrice: 488.65676400143957, averageDeliveryTime: 10.963459128082302},
		{BusinessUnit: 'LUXURY SPECIALTIES',Type: 'JEWELRY', averagePrice: 567.9144725864594, averageDeliveryTime: 10.49772537661152},
		{BusinessUnit: 'LUXURY SPECIALTIES',Type: 'MUSICAL INSTRUMENT', averagePrice: 392.40989424403296, averageDeliveryTime: 10.579943986958158},
		{BusinessUnit: 'LUXURY SPECIALTIES',Type: 'POTIONS & SCROLLS', averagePrice: 482.1204252378094, averageDeliveryTime: 10.92033611611284},
		{BusinessUnit: 'LUXURY SPECIALTIES',Type: 'SUMMONING DEVICE', averagePrice: 496.92728393343543, averageDeliveryTime: 10.908503489273714},
		{BusinessUnit: 'LUXURY SPECIALTIES',Type: 'TOOLS & KITS', averagePrice: 549.8910355486862, averageDeliveryTime: 11.488469860896446},
  ];

	let isLuxuryHidden = false;
	let isAdventuringHidden = false;
	let isComissionHidden = false;
	let isJewleryHidden = false;
	let isAEHidden = false;
	let isATHidden = false;
	let isAAHidden = false;
	let isMIHidden = false;
	let isPSHidden = false;
	let isSDHidden = false;
	let isTKHidden = false;
	
	let data = data_orig; 

	  // Define colors for each type
  const colorScale = {
    'ARMS & ARMOUR': '#de6673',
    'ADVENTURING EQUIPMENT': '#559f87',
    'TOOLS & KITS': '#ff9f41',
    'POTIONS & SCROLLS': '#8ff281',
    'ANIMALS & TRANSPORTATION': '#ffcb39',
    'JEWELRY': '#5dbfe1',
    'SUMMONING DEVICE': '#d43db7',
    'MUSICAL INSTRUMENT': '#1668c2'
  };

  onMount(() => {
    const margin = { top: 20, right: 30, bottom: 30, left: 60 };
    const width = 600 - margin.left - margin.right;
    const height = 400 - margin.top - margin.bottom;

    const svg = d3.select('#chart')
      // .attr('width', width + margin.left + margin.right)
			.attr('width', 1000) 
      .attr('height', height + margin.top + margin.bottom)
      .append('g')
      .attr('transform', `translate(${margin.left},${margin.top})`);

    const xScalePrice = d3.scaleLinear()
      .domain([-d3.max(data, d => d.averagePrice), 0])
      .range([0, width / 2]);

    const xScaleDelivery = d3.scaleLinear()
      .domain([0, d3.max(data, d => d.averageDeliveryTime)])
      .range([0, width / 2]);

    const yScale = d3.scaleBand()
      .domain(data.map(d => `${d.BusinessUnit}-${d.Type}`)) 
      .range([height, 0])  
      .padding(0.1);

    // const colorScale = d3.scaleOrdinal()
     // .domain(data.map(d => d.Type))
     //  .range(d3.schemeCategory10);

			// Function to update the chart based on selected BusinessUnit Lux
    function updateChart() { 
        isLuxuryHidden = !isLuxuryHidden; 

				if (isLuxuryHidden) {
	        const filteredData = isLuxuryHidden ? data.filter(d => d.BusinessUnit !== 'LUXURY SPECIALTIES') : data;
					
	        svg.selectAll('.bar-price')
	            .data(filteredData, d => `${d.BusinessUnit}-${d.Type}`)    
	            .exit()
	            .remove();
	
	        svg.selectAll('.bar-delivery')
	            .data(filteredData, d => `${d.BusinessUnit}-${d.Type}`)
	            .exit() 
	            .remove();
				}else { 
					data_orig.forEach(row => {
					    if (row.BusinessUnit === 'LUXURY SPECIALTIES') {
					        data.push(row);
					    }
					});
					drawChart();
				}
		}

			// Function to update the chart based on selected BusinessUnit
    function updateChartA() { 
				isAdventuringHidden = !isAdventuringHidden; 

				if (isAdventuringHidden) {
	        const filteredData = isAdventuringHidden ? data.filter(d => d.BusinessUnit !== 'ADVENTURING') : data; 
	        svg.selectAll('.bar-price')
	            .data(filteredData, d => `${d.BusinessUnit}-${d.Type}`) 
	            .exit() 
	            .remove(); 
	
	        svg.selectAll('.bar-delivery')
	            .data(filteredData, d => `${d.BusinessUnit}-${d.Type}`)
	            .exit() 
	            .remove();
				}else { 
					data_orig.forEach(row => {
					    if (row.BusinessUnit === 'ADVENTURING') {
					        data.push(row);
					    }
					});
					drawChart();
				}
		}


			// Function to update the chart based on selected BusinessUnit 
    function updateChartC() {  
				isComissionHidden = !isComissionHidden;

				if (isComissionHidden) {
	        const filteredData = isComissionHidden ? data.filter(d => d.BusinessUnit !== 'COMMISSIONS') : data;
					
	        svg.selectAll('.bar-price')
	            .data(filteredData, d => `${d.BusinessUnit}-${d.Type}`) 
	            .exit()
	            .remove(); 
	
	        svg.selectAll('.bar-delivery')
	            .data(filteredData, d => `${d.BusinessUnit}-${d.Type}`)  
	            .exit() 
	            .remove();
				}else { 
	        data_orig.forEach(row => {
					    if (row.BusinessUnit === 'COMMISSIONS') {
					        data.push(row);
					    }
					});
					drawChart();
				}
		}

		function updateChartAE() {  
				isAEHidden = !isAEHidden;

			if (isAEHidden) {
		        const filteredData = isAEHidden ? data.filter(d => d.Type !== 'ADVENTURING EQUIPMENT') : data;
						
		        svg.selectAll('.bar-price')
		            .data(filteredData, d => `${d.BusinessUnit}-${d.Type}`) 
		            .exit()
		            .remove(); 
		
		        svg.selectAll('.bar-delivery')
		            .data(filteredData, d => `${d.BusinessUnit}-${d.Type}`)  
		            .exit() 
		            .remove(); 
					}else { 
		        data_orig.forEach(row => {
						    if (row.Type === 'ADVENTURING EQUIPMENT') {
						        data.push(row);
						    }
						});
						drawChart();
					}
			}

		function updateChartAT() {  
				isATHidden = !isATHidden;

			if (isATHidden) {
		        const filteredData = isATHidden ? data.filter(d => d.Type !== 'ANIMALS & TRANSPORTATION') : data;
						
		        svg.selectAll('.bar-price')
		            .data(filteredData, d => `${d.BusinessUnit}-${d.Type}`) 
		            .exit()
		            .remove(); 
		
		        svg.selectAll('.bar-delivery')
		            .data(filteredData, d => `${d.BusinessUnit}-${d.Type}`)  
		            .exit() 
		            .remove(); 
					}else { 
		        data_orig.forEach(row => {
						    if (row.Type === 'ANIMALS & TRANSPORTATION') {
						        data.push(row);
						    }
						});
						drawChart();
					}
			}

		function updateChartAA() {  
				isAAHidden = !isAAHidden;

			if (isAAHidden) {
		        const filteredData = isAAHidden ? data.filter(d => d.Type !== 'ARMS & ARMOUR') : data;
						
		        svg.selectAll('.bar-price')
		            .data(filteredData, d => `${d.BusinessUnit}-${d.Type}`) 
		            .exit()
		            .remove(); 
		
		        svg.selectAll('.bar-delivery')
		            .data(filteredData, d => `${d.BusinessUnit}-${d.Type}`)  
		            .exit() 
		            .remove(); 
					}else { 
		        data_orig.forEach(row => {
						    if (row.Type === 'ARMS & ARMOUR') {
						        data.push(row);
						    }
						});
						drawChart();
					}
			}

		function updateChartJewlery() {  
				isJewleryHidden = !isJewleryHidden;

			if (isJewleryHidden) {
		        const filteredData = isJewleryHidden ? data.filter(d => d.Type !== 'JEWELRY') : data;
						
		        svg.selectAll('.bar-price')
		            .data(filteredData, d => `${d.BusinessUnit}-${d.Type}`) 
		            .exit()
		            .remove(); 
		
		        svg.selectAll('.bar-delivery')
		            .data(filteredData, d => `${d.BusinessUnit}-${d.Type}`)  
		            .exit() 
		            .remove(); 
					}else { 
		        data_orig.forEach(row => {
						    if (row.Type === 'JEWELRY') {
						        data.push(row);
						    }
						});
						drawChart();
					}
			}

		function updateChartMI() {  
				isMIHidden = !isMIHidden;

			if (isMIHidden) {
		        const filteredData = isMIHidden ? data.filter(d => d.Type !== 'MUSICAL INSTRUMENT') : data;
						
		        svg.selectAll('.bar-price')
		            .data(filteredData, d => `${d.BusinessUnit}-${d.Type}`) 
		            .exit()
		            .remove(); 
		
		        svg.selectAll('.bar-delivery')
		            .data(filteredData, d => `${d.BusinessUnit}-${d.Type}`)  
		            .exit() 
		            .remove(); 
					}else { 
		        data_orig.forEach(row => {
						    if (row.Type === 'MUSICAL INSTRUMENT') {
						        data.push(row);
						    }
						});
						drawChart();
					}
			}

		function updateChartPS() {  
				isPSHidden = !isPSHidden;

			if (isPSHidden) {
		        const filteredData = isPSHidden ? data.filter(d => d.Type !== 'POTIONS & SCROLLS') : data;
						
		        svg.selectAll('.bar-price')
		            .data(filteredData, d => `${d.BusinessUnit}-${d.Type}`) 
		            .exit()
		            .remove(); 
		
		        svg.selectAll('.bar-delivery')
		            .data(filteredData, d => `${d.BusinessUnit}-${d.Type}`)  
		            .exit() 
		            .remove(); 
					}else { 
		        data_orig.forEach(row => {
						    if (row.Type === 'POTIONS & SCROLLS') {
						        data.push(row);
						    }
						});
						drawChart();
					}
			}

		function updateChartSD() {  
				isSDHidden = !isSDHidden;

			if (isSDHidden) {
		        const filteredData = isSDHidden ? data.filter(d => d.Type !== 'SUMMONING DEVICE') : data;
						
		        svg.selectAll('.bar-price')
		            .data(filteredData, d => `${d.BusinessUnit}-${d.Type}`) 
		            .exit()
		            .remove(); 
		
		        svg.selectAll('.bar-delivery')
		            .data(filteredData, d => `${d.BusinessUnit}-${d.Type}`)  
		            .exit() 
		            .remove(); 
					}else { 
		        data_orig.forEach(row => {
						    if (row.Type === 'SUMMONING DEVICE') {
						        data.push(row);
						    }
						});
						drawChart();
					}
			}

		function updateChartTK() {   
				isTKHidden = !isTKHidden;

			if (isTKHidden) {
		        const filteredData = isTKHidden ? data.filter(d => d.Type !== 'TOOLS & KITS') : data;
						
		        svg.selectAll('.bar-price')
		            .data(filteredData, d => `${d.BusinessUnit}-${d.Type}`) 
		            .exit()
		            .remove(); 
		
		        svg.selectAll('.bar-delivery')
		            .data(filteredData, d => `${d.BusinessUnit}-${d.Type}`)  
		            .exit() 
		            .remove(); 
					}else { 
		        data_orig.forEach(row => {
						    if (row.Type === 'TOOLS & KITS') {
						        data.push(row);
						    }
						});
						drawChart();
					}
			}
	

    // Buttons for Lux 
    const buttonLux = svg.append('g')
      .attr('class', 'buttonLux')
      .attr('transform', `translate(${ -50}, ${50})`) 
      .on('click', updateChart);

    buttonLux.append('rect')
      .attr('width', 110)
      .attr('height', 30) 
      .attr('fill', 'lightblue') 
      .attr('rx', 5)  
      .attr('ry', 5);

    buttonLux.append('text')
      .attr('x', 55) 
      .attr('y', 18)
      .attr('text-anchor', 'middle')
      .attr('alignment-baseline', 'middle')
      .attr('fill', 'black')
      .style('font-size', '10px')
      .style('font-family', 'Segoe UI, Tahoma, Geneva, Verdana, sans-serif') 
      .text('LUXURY SPECIALTIES');

		// Buttons for Adventuring
    const buttonAdv = svg.append('g')
      .attr('class', 'buttonAdv')
      .attr('transform', `translate(${ -50}, ${280})`)  
      .on('click', updateChartA);

    buttonAdv.append('rect')
      .attr('width', 110)
      .attr('height', 30) 
      .attr('fill', 'lightblue') 
      .attr('rx', 5)  
      .attr('ry', 5);

    buttonAdv.append('text')
      .attr('x', 55) 
      .attr('y', 18)
      .attr('text-anchor', 'middle')
      .attr('alignment-baseline', 'middle')
      .attr('fill', 'black')
      .style('font-size', '10px')
      .style('font-family', 'Segoe UI, Tahoma, Geneva, Verdana, sans-serif') 
      .text('ADVENTURING');

		// Buttons for Comission
    const buttonCom = svg.append('g')
      .attr('class', 'buttonCom')
      .attr('transform', `translate(${ -50}, ${170})`)    
      .on('click', updateChartC); 

    buttonCom.append('rect')
      .attr('width', 110)
      .attr('height', 30) 
      .attr('fill', 'lightblue') 
      .attr('rx', 5)  
      .attr('ry', 5);

    buttonCom.append('text')
      .attr('x', 55) 
      .attr('y', 18)
      .attr('text-anchor', 'middle')
      .attr('alignment-baseline', 'middle')
      .attr('fill', 'black')
      .style('font-size', '10px')
      .style('font-family', 'Segoe UI, Tahoma, Geneva, Verdana, sans-serif') 
      .text('COMISSION'); 
		
		// Button for adventuring equipments 
		const buttonAE = svg.append('g') 
      .attr('class', 'buttonAE')
      .attr('transform', `translate(${550}, ${300})`)   
      .on('click', updateChartAE); 

    buttonAE.append('rect') 
      .attr('width', 180)
      .attr('height', 30) 
      .attr('fill', '#559f87') 
      .attr('rx', 5)  
      .attr('ry', 5);

    buttonAE.append('text')
      .attr('x', 90) 
      .attr('y', 18)
      .attr('text-anchor', 'middle')
      .attr('alignment-baseline', 'middle')
      .attr('fill', 'black')
      .style('font-size', '12px')
      .style('font-family', 'Segoe UI, Tahoma, Geneva, Verdana, sans-serif') 
      .text('ADVENTURING EQUIPMENT'); 

		// Button for animals and transportation
		const buttonAT = svg.append('g')
      .attr('class', 'buttonAT')
      .attr('transform', `translate(${550}, ${260})`) 
      .on('click', updateChartAT);

    buttonAT.append('rect')
      .attr('width', 180)
      .attr('height', 30) 
      .attr('fill', '#ffcb39') 
      .attr('rx', 5)  
      .attr('ry', 5);

    buttonAT.append('text')
      .attr('x', 90) 
      .attr('y', 18)
      .attr('text-anchor', 'middle')
      .attr('alignment-baseline', 'middle')
      .attr('fill', 'black')
      .style('font-size', '12px')
      .style('font-family', 'Segoe UI, Tahoma, Geneva, Verdana, sans-serif') 
      .text('ANIMALS & TRANSPORTATION'); 

		// Button for arms and armour
		const buttonAA = svg.append('g')
      .attr('class', 'buttonAA')
      .attr('transform', `translate(${550}, ${220})`) 
      .on('click', updateChartAA);

    buttonAA.append('rect')
      .attr('width', 180)
      .attr('height', 30) 
      .attr('fill', '#de6673') 
      .attr('rx', 5)  
      .attr('ry', 5);

    buttonAA.append('text')
      .attr('x', 90) 
      .attr('y', 18)
      .attr('text-anchor', 'middle')
      .attr('alignment-baseline', 'middle')
      .attr('fill', 'black')
      .style('font-size', '12px')
      .style('font-family', 'Segoe UI, Tahoma, Geneva, Verdana, sans-serif') 
      .text('ARMS & ARMOUR'); 

		// Button for Jewelery
		const buttonJewelery = svg.append('g')
      .attr('class', 'buttonJewelery')
      .attr('transform', `translate(${550}, ${180})`) 
      .on('click', updateChartJewlery);

    buttonJewelery.append('rect')
      .attr('width', 180)
      .attr('height', 30) 
      .attr('fill', '#5dbfe1') 
      .attr('rx', 5)   
      .attr('ry', 5);

    buttonJewelery.append('text')
      .attr('x', 90) 
      .attr('y', 18)
      .attr('text-anchor', 'middle')
      .attr('alignment-baseline', 'middle')
      .attr('fill', 'black')
      .style('font-size', '12px')
      .style('font-family', 'Segoe UI, Tahoma, Geneva, Verdana, sans-serif') 
      .text('JEWLERY'); 

		// Button for musical instruments
		const buttonMI = svg.append('g')
      .attr('class', 'buttonMI')
      .attr('transform', `translate(${550}, ${140})`) 
      .on('click', updateChartMI);

    buttonMI.append('rect')
      .attr('width', 180)
      .attr('height', 30) 
      .attr('fill', '#1668c2') 
      .attr('rx', 5)  
      .attr('ry', 5);

    buttonMI.append('text')
      .attr('x', 90) 
      .attr('y', 18)
      .attr('text-anchor', 'middle')
      .attr('alignment-baseline', 'middle')
      .attr('fill', 'black')
      .style('font-size', '12px')
      .style('font-family', 'Segoe UI, Tahoma, Geneva, Verdana, sans-serif') 
      .text('MUSICAL INSTRUMENTS'); 

		// Button for potions and scrolls
		const buttonPS = svg.append('g')
      .attr('class', 'buttonPS')
      .attr('transform', `translate(${550}, ${100})`)  
      .on('click', updateChartPS);

    buttonPS.append('rect')
      .attr('width', 180)
      .attr('height', 30) 
      .attr('fill', '#8ff281') 
      .attr('rx', 5)  
      .attr('ry', 5);

    buttonPS.append('text')
      .attr('x', 90) 
      .attr('y', 18)
      .attr('text-anchor', 'middle')
      .attr('alignment-baseline', 'middle')
      .attr('fill', 'black')
      .style('font-size', '12px')
      .style('font-family', 'Segoe UI, Tahoma, Geneva, Verdana, sans-serif') 
      .text('POTIONS & SCROLLS'); 

		// Button for summoning devices
		const buttonSD = svg.append('g')
      .attr('class', 'buttonSD')
      .attr('transform', `translate(${550}, ${60})`) 
      .on('click', updateChartSD);

    buttonSD.append('rect')
      .attr('width', 180)
      .attr('height', 30) 
      .attr('fill', '#d43db7') 
      .attr('rx', 5)  
      .attr('ry', 5);

    buttonSD.append('text')
      .attr('x', 90) 
      .attr('y', 18)
      .attr('text-anchor', 'middle')
      .attr('alignment-baseline', 'middle')
      .attr('fill', 'black') 
      .style('font-size', '12px')
      .style('font-family', 'Segoe UI, Tahoma, Geneva, Verdana, sans-serif') 
      .text('SUMMONING DEVICE'); 

		// Button for tools and kits
		const buttonTK = svg.append('g')
      .attr('class', 'buttonTK')
      .attr('transform', `translate(${550}, ${20})`) 
      .on('click', updateChartTK);

    buttonTK.append('rect')
      .attr('width', 180)
      .attr('height', 30) 
      .attr('fill', '#ff9f41') 
      .attr('rx', 5)  
      .attr('ry', 5);

    buttonTK.append('text') 
      .attr('x', 90) 
      .attr('y', 18)
      .attr('text-anchor', 'middle')
      .attr('alignment-baseline', 'middle')
      .attr('fill', 'black')
      .style('font-size', '12px')
      .style('font-family', 'Segoe UI, Tahoma, Geneva, Verdana, sans-serif') 
      .text('TOOLS AND KITS'); 
 

    // Draw the initial chart
    drawChart();

    function drawChart() {
		
			svg.selectAll('.bar-price')
      .data(data)
      .enter().append('rect')
      .attr('class', 'bar-price')
      .attr('x', d => xScalePrice(-d.averagePrice))
      .attr('y', d => yScale(`${d.BusinessUnit}-${d.Type}`) + yScale.bandwidth() / 2)  
			.attr('width', d => Math.abs(xScalePrice(0) - xScalePrice(d.averagePrice))) 
      .attr('height', yScale.bandwidth() / 2)
      .style('fill', d => colorScale[d.Type]);  

    svg.selectAll('.bar-delivery')
      .data(data)
      .enter().append('rect')
      .attr('class', 'bar-delivery')
      .attr('x', width / 2)
      .attr('y', d => yScale(`${d.BusinessUnit}-${d.Type}`) + yScale.bandwidth() / 2) 
      .attr('width', d => xScaleDelivery(d.averageDeliveryTime)) 
      .attr('height', yScale.bandwidth() / 2)
      .style('fill', d => colorScale[d.Type]);


    svg.append('g')
      .attr('class', 'x-axis-price')
      .attr('transform', `translate(0,${height})`)
      .call(d3.axisBottom(xScalePrice).tickFormat(d => Math.abs(d)));

    svg.append('g')
      .attr('class', 'x-axis-delivery')
      .attr('transform', `translate(${width / 2},${height})`)
      .call(d3.axisBottom(xScaleDelivery));

			// Add label for price axis
		svg.append("text")
		  .attr("x", width / 4 - 100) // Adjust position as needed
		  .attr("y", height + margin.top + 8) // Adjust position as needed  
		  .attr("text-anchor", "middle")
			.style("fill", "black")
			.style('font-size', '12px')
      .style('font-family', 'Segoe UI, Tahoma, Geneva, Verdana, sans-serif') 
		  .text("Average Price per Product (CP)"); 
		
		// Add label for delivery time axis
		svg.append("text")
		  .attr("x", 3 * width / 4 + 120) // Adjust position as needed
		  .attr("y", height + margin.top + 8) // Adjust position as needed
	    .attr("text-anchor", "middle")
			.style("fill", "black")
			.style('font-size', '12px')
      .style('font-family', 'Segoe UI, Tahoma, Geneva, Verdana, sans-serif') 
	    .text("Average Delivery Time (days)"); 

    svg.append('g')
      .attr('class', 'y-axis')
			.attr('transform', `translate(${xScalePrice(0)},0)`) // Move y-axis to zero on x-axis
      .call(d3.axisLeft(yScale).tickSize(0).tickFormat('')); // remove the labels from the y axis

    // Remove tick marks for y-axis
    svg.selectAll('.y-axis .tick line').remove();

			// Append a single title for all legends
		svg.append('text')
		    .attr('x', width + margin.right / 4 + 40)
		    .attr('y', +10) // Adjust this value as needed for positioning
		    .attr('fill', 'black')
				.style('font-size', '20px')
        
		    .text("Types of Products"); 

		// Append a single title for business unit
		svg.append('text')
		    .attr('x', -55)
		    .attr('y', +10) // Adjust this value as needed for positioning
		    .attr('fill', 'black')
				.style('font-size', '20px')
        .style('font-family', 'Segoe UI, Tahoma, Geneva, Verdana, sans-serif') 
		    .text("Business Unit")

			// Add white lines parallel to the x-axis
			const line1Y = 131; // Adjust the y-coordinate of the first line
			const line2Y = 227; // Adjust the y-coordinate of the second line
			const lineWidth = width; // Adjust the width of the lines to cover the entire width of the SVG
			
			svg.append('line')
			  .attr('x1', 0) // Starting x-coordinate
			  .attr('y1', line1Y) // Starting y-coordinate
			  .attr('x2', lineWidth) // Ending x-coordinate
			  .attr('y2', line1Y) // Ending y-coordinate
			  .style('stroke', 'black') // Line color
			  .style('stroke-width', 2); // Line width 
			
			svg.append('line')
			  .attr('x1', 0) // Starting x-coordinate 
			  .attr('y1', line2Y) // Starting y-coordinate
			  .attr('x2', lineWidth) // Ending x-coordinate
			  .attr('y2', line2Y) // Ending y-coordinate
			  .style('stroke', 'black') // Line color
			  .style('stroke-width', 2); // Line width
    }
  });
</script>
<h1 style="margin-top: 2px; margin-left: 0px; font-size: 24px;'font-family', 'Segoe UI, Tahoma, Geneva, Verdana, sans-serif') ">Average Delivery Time and Average Price for Product Types Beloning to Different Business Units</h1>
<svg id="chart"></svg>