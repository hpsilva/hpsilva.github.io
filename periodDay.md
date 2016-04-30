---
layout: page
title: Market Snapshot
---
<meta charset="utf-8">

<head>
  <style>
    @import url(http://fonts.googleapis.com/css?family=Yanone+Kaffeesatz:400,700);

    body {
    font-family: "Yanone Kaffeesatz";
    }
    
    #demo {
    font-family: "Yanone Kaffeesatz";
    font-size:12px;
    }
    
    .group {
      margin-bottom: 1em;
    }
    
    /*
    .axis {
      font: 8px sans-serif;
      position: fixed;
      pointer-events: none;
      z-index: 2;
    }
    
    .axis text {
      -webkit-transition: fill-opacity 250ms linear;
    }
    
    .axis path {
      display: none;
    }
    
    .axis line {
      stroke: #000;
      shape-rendering: crispEdges;
    }
    
    .axis.top {
      background-image: linear-gradient(top, #fff 0%, rgba(255,255,255,0) 100%);
      background-image: -o-linear-gradient(top, #fff 0%, rgba(255,255,255,0) 100%);
      background-image: -moz-linear-gradient(top, #fff 0%, rgba(255,255,255,0) 100%);
      background-image: -webkit-linear-gradient(top, #fff 0%, rgba(255,255,255,0) 100%);
      background-image: -ms-linear-gradient(top, #fff 0%, rgba(255,255,255,0) 100%);
      top: 0px;
      padding: 0 0 24px 0;
    }
    
    .axis.bottom {
      background-image: linear-gradient(bottom, #fff 0%, rgba(255,255,255,0) 100%);
      background-image: -o-linear-gradient(bottom, #fff 0%, rgba(255,255,255,0) 100%);
      background-image: -moz-linear-gradient(bottom, #fff 0%, rgba(255,255,255,0) 100%);
      background-image: -webkit-linear-gradient(bottom, #fff 0%, rgba(255,255,255,0) 100%);
      background-image: -ms-linear-gradient(bottom, #fff 0%, rgba(255,255,255,0) 100%);
      bottom: 0px;
      padding: 24px 0 0 0;
    }
    */
    
    .horizon {
      border-bottom: solid 1px #000;
      overflow: hidden;
      position: relative;
    }
    
    .horizon {
      border-top: solid 1px #000;
      border-bottom: solid 1px #000;
    }
    
    .horizon + .horizon {
      border-top: none;
    }
    
    .horizon canvas {
      display: block;
    }
    
    .horizon .title,
    .horizon .value {
      bottom: 0;
      line-height: 30px;
      margin: 0 6px;
      position: absolute;
      text-shadow: 0 1px 0 rgba(255,255,255,.5);
      white-space: nowrap;
    }
    
    .horizon .title {
      left: 0;
    }
    
    .horizon .value {
      right: 0;
    }
    
    .line {
      background: #000;
      z-index: 2;
    }
  </style>
  
  <script src="//d3js.org/d3.v2.min.js" charset="utf-8"></script>
  <script src="https://square.github.io/cubism/cubism.v1.min.js"></script>
</head>

<div id="demo">
  <script>
    // Create Context
    var context = cubism.context()
        .serverDelay(0) // Collection lag
        .step(24 * 60 * 60 * 1000) // step(60 * 60 * 1000) - sixty minutes per value
        .size(750) // 1420 Number of Observation to parse
        .stop();
        
    alert( 'Bit of patience required...' )
    
    // Add Ruler
    d3.select("#demo").selectAll(".axis")
        .data(["top", "bottom"])
      .enter().append("div")
        .attr("class", function(d) { return d + " axis"; })
        .each(function(d) { d3.select(this).call(context.axis().ticks(12).orient(d)); });
    
    // Add vertical line
    d3.select("#demo").append("div")
        .attr("class", "rule")
        .call(context.rule());
    
    // Plot Horizon Graphs
    d3.select("#demo").selectAll(".horizon")
        .data([ 'DE10YB_EUR', 'UK10YB_GBP', 'USB02Y_USD', 'USB05Y_USD', 'USB10Y_USD', 'USB30Y_USD',
                'AU200_AUD', 'CH20_CHF', 'DE30_EUR', 'EU50_EUR', 'FR40_EUR', 'HK33_HKD', 'SG30_SGD',
                'JP225_USD', 'NAS100_USD', 'NL25_EUR', 'SPX500_USD', 'UK100_GBP', 'US2000_USD', 'US30_USD',
                'BCO_USD', 'CORN_USD','NATGAS_USD', 'SOYBN_USD', 'SUGAR_USD', 'WHEAT_USD', 'WTICO_USD', 
                'XAG_USD', 'XAU_USD','XAU_XAG', 'XCU_USD', 'XPD_USD', 'XPT_USD', 'USD_CAD', 'USD_CHF', 
                'USD_CNH', 'USD_CZK', 'USD_DKK', 'USD_HKD', 'USD_HUF', 'USD_INR', 'USD_JPY', 'USD_MXN',
                'USD_NOK', 'USD_PLN', 'USD_SAR', 'USD_SEK', 'USD_SGD', 'USD_THB', 'USD_TRY', 'USD_ZAR' ].map(stock))
      .enter().insert("div", ".bottom")
        .attr("class", "horizon")
      .call(context.horizon()
        .format(d3.format("+,.2p"))
        .height(25));
    
    // Set Focus on the Ruler / Axis
    context.on("focus", function(i) {
      d3.selectAll(".value").style("right", i == null ? null : context.size() - i + "px");
    });
    
    // Create Metrics by Reading from CSV file
    function stock(name) {
      var format = d3.time.format("%Y-%m-%d");
      return context.metric(function(start, stop, step, callback) {
          d3.csv("/js/cubism/snapshot.csv", function(rows) {
              rows = rows.map(function(d) {
                  return [format.parse(d.Date), +d[name]];
              }).filter(function(d) {
                  return d[1];
              }).reverse();
              var date = rows[0][0],
                  compare = rows[0][1],
                  value = rows[0][1],
                  values = [value];
              rows.forEach(function(d) {
                  while ((date = d3.time.day.offset(date, 1)) < d[0]) values.push(value);
                  values.push(value = (d[1] - compare) / compare);
              });
              callback(null, values.slice(-context.size()));
          });
      }, name);
    }

  </script>
</div>
