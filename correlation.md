---
layout: page
title: Correlations
---

<html class="miner">
<meta charset="utf-8">

<style>
    @import url(http://fonts.googleapis.com/css?family=Yanone+Kaffeesatz:400,700);
</style>

<style> @import url(cooccurrence.css); </style>
<!-- <script src="d3.v2.8.1.min.js"></script> -->

<h1>Word Co-occurrence of Documents</h1>

<p>Each cell in this heat map matrix is shaded proportional the product of the number of occurrences of each pair of words in the same document summed over all the documents (the product of the occurrence matrix with its transpose).</a></i>.

<p>Sort by: <select id="matrixsortorder">
  <option value="alphabetic">Alphabetic</option>
  <option value="frequency">Frequency</option>
  <option value="cluster">Cluster</option>
</select>

<div id="matrix"></div>

<script type="text/javascript" src="//cdnjs.cloudflare.com/ajax/libs/d3/3.5.3/d3.min.js"></script>
<!-- <script type="text/javascript" src="cdnjs.cloudflare.com/ajax/libs/underscore.js/1.7.0/underscore-min.js"></script> -->
<script src="graphutil.js"></script>
<script>

var graph;
d3.json("word_cooccurrence.json", function(error, json) {
    if (error) return console.warn(error);
    graph = json;
    draw_matrix_heat_map(graph, 900, 900, "#matrix");
        //,function (group_num) { var groups = ["", "Whig", "Democratic", "Republican", "Democratic-Republican", "Federalist"]; return groups[group_num]; },
        //function (name) { return name.substring(0,4) + "\n" + name.substring(5,30); }
    //);
});

</script>


<p>This dynamic visualization uses <a href="http://d3js.org/">d3.js</a> by <a href="http://bost.ocks.org/">Mike Bostock</a>.
</aside>
