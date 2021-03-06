---
layout: page
title: Market Snapshot
---
<meta charset="utf-8">

<style>
@import url(http://fonts.googleapis.com/css?family=Yanone+Kaffeesatz:400,700);

body {
  font-family: Yanone Kaffeesatz;
  font-size: 13px;
  margin: 30px auto;
  width: 1280px;
  position: relative;
}

header {
  padding: 6px 0;
}

.group {
  margin-bottom: 1em;
}

.axis {
  font: 10px sans-serif;
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


<body id="graph">
  <script>
    //alert( 'On mobile, zoom out...' )
  
    // Create Context
    var context = cubism.context()
        .serverDelay(0)
        .step(24 * 60 * 60 * 1000)
        .size(1280)
        .stop();
    
    // Add Ruler
    d3.select("#graph").selectAll(".axis")
        .data(["top", "bottom"])
      .enter().append("div")
        .attr("class", function(d) { return d + " axis"; })
        .each(function(d) { d3.select(this).call(context.axis().ticks(12).orient(d)); });
    
    // Add vertical line
    d3.select("#graph").append("div")
        .attr("class", "rule")
        .call(context.rule());
    
    // Plot Horizon Graphs
    d3.select("#graph").selectAll(".horizon")
        .data([ 'Bund', 'UK 10Y Gilt', 'US 2Y T-Note', 'US 5Y T-Note', 'US 10Y T-Note', 'US T-Bond', 'Australia 200',
                'Germany 30', 'Europe 50', 'France 40', 'Hong Kong 33', 'Japan 225', 'Netherlands 25', 'Singapore 30',
                'Swiss 20', 'UK 100', 'US Nas 100', 'US SPX 500', 'US Russ 2000', 'US Wall St 30', 'Brent Crude Oil',
                'Corn', 'Natural Gas', 'Soybeans', 'Sugar', 'Wheat', 'West Texas Oil', 'Copper', 'Gold', 'Gold/Silver',
                'Palladium', 'Platinum', 'Silver', 'EUR/USD', 'USD/CAD', 'USD/CHF', 'USD/CNH', 'USD/CZK', 'USD/DKK',
                'USD/HKD', 'USD/HUF', 'USD/INR', 'USD/JPY', 'USD/MXN', 'USD/NOK', 'USD/PLN', 'USD/SAR', 'USD/SEK',
                'USD/SGD', 'USD/THB', 'USD/TRY', 'USD/ZAR'].map(stock))
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
                  compare = rows[943][1],
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
</body>
