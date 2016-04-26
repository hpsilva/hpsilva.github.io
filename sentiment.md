---
layout: page
title: Test
subtitle: This is a test!
---

<meta charset="utf-8">

<style>
    @import url(http://fonts.googleapis.com/css?family=Yanone+Kaffeesatz:400,700);
    @import url(/js/cubism/style.css);
</style>

<body>
    <h1> Cubism Example: </h1>
    <script src="/js/cubism/d3.v2.js"></script>
    <script src="/js/cubism/cubism.v1.js"></script>
</body>

<script>
    var context = cubism.context()
        .step(1e4)
        .size(1440);
    
    // Add AXIS on TOP and BOTTOM
    d3.select("body").selectAll(".axis")
        .data(["top", "bottom"])
      .enter().append("div")
        .attr( "class", function(d) { return d + " axis"; } )
        .each( function(d) { d3.select(this).call(context.axis().ticks(12).orient(d)); } );
    
    // Add RULER LINE
    d3.select("body").append("div")
        .attr("class", "rule")
        .call(context.rule());
    
    // Add the different cubism graphic lines
    d3.select("body").selectAll(".horizon")
        .data(d3.range(1, 10).map(random))
      .enter().insert("div", ".bottom")
        .attr("class", "horizon")
        .call( context.horizon().extent([-10, 10]).height(120) );
        
    
    // On mousemove, reposition the chart values to match the rule.
    context.on("focus", function(i) {
      d3.selectAll(".value").style("right", i == null ? null : context.size() - i + "px");
    });
    
    // Replace this with context.graphite and graphite.metric!
    function random(x) {
      var value = 0,
          values = [],
          i = 0,
          last;
      return context.metric(function(start, stop, step, callback) {
        start = +start, stop = +stop;
        if (isNaN(last)) last = start;
        while (last < stop) {
          last += step;
          value = Math.max(-10, Math.min(10, value + .8 * Math.random() - .4 + .2 * Math.cos(i += x * .02)));
          values.push(value);
        }
        callback(null, values = values.slice((start - stop) / step));
      }, x);
    }
</script>


<style>

</style>
