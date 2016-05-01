---
layout: page
title: Correlations
---

<html class="miner">
<meta charset="utf-8">

<style>
    @import url(http://fonts.googleapis.com/css?family=Yanone+Kaffeesatz:400,700);
    @import url(http://fonts.googleapis.com/css?family=Droid+Serif|Droid+Serif:b|Droid+Serif:i|Lato|Lato:b|Lato:i);
    
    /*
    html { min-width: 1000px; }
    */
    
    a { color: #57A; }
    
    .background { fill: #eee; }
    
    body > p, li > p { line-height: 1.4em; }
    
    body > p { width: 700px; }
    
    svg { font: 9px sans-serif; }
    
    .axis path, .axis line {
      fill: none;
      stroke: #000;
      shape-rendering: crispEdges;
    }
    
    line { stroke: #fff; }
    
    text.active { 
        fill: red; 
        font-size: 13px; 
        font-weight: 900; 
        letter-spacing: -.05em;
    }
    
    .miner aside, .miner h1 { font-family: "Lato", sans-serif; }
    
    .miner h1 { color: #430; }
    
    .miner body {
      color: #430;
      }
</style>
<!-- <script src="d3.v2.8.1.min.js"></script> -->

<p>Sort by: <select id="matrixsortorder">
  <option value="alphabetic">Alphabetic</option>
  <option value="frequency">Frequency</option>
  <option value="cluster">Cluster</option>
</select>

<div id="matrix"></div>

<script type="text/javascript" src="//cdnjs.cloudflare.com/ajax/libs/d3/3.5.3/d3.min.js"></script>
<!-- <script type="text/javascript" src="cdnjs.cloudflare.com/ajax/libs/underscore.js/1.7.0/underscore-min.js"></script> -->
<script src="/js/correlation/graphutil.js"></script>

<script>
    var graph;
    d3.json("/js/correlation/correlatio.json", function(error, json) {
        if (error) return console.warn(error);
        graph = json;
        draw_matrix_heat_map(graph, 900, 900, "#matrix");
            //,function (group_num) { var groups = ["", "Whig", "Democratic", "Republican", "Democratic-Republican", "Federalist"]; return groups[group_num]; },
            //function (name) { return name.substring(0,4) + "\n" + name.substring(5,30); }
        //);
    });
</script>

<h6>Viz powered by <a href="http://d3js.org/">d3.js</a> from <a href="http://bost.ocks.org/">Mike Bostock</h6>.
