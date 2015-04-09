## 2015 Space Apps NYC
## Intro to NASA Open Data APIs
![Socrata](img/snu-astronaut.png)
===

<h1>Who the heck<br />are you?</h1>
![Socrata](/presentations/img/socrata-white-medium.png)

---

<img class="fullscreen-img" src="/presentations/img/at_table.jpg" />

<h2>We build <span class="toy-store-blue">software</span> to make data <span class="blushing-salmon">more useful</span> to <span class="golden">more people</span>.</h2>

<!-- https://www.flickr.com/photos/hyku/2497370097 -->
--- 

<img class="fullscreen-img" src="/presentations/img/city.jpg" />

<h2>We believe that <span class="toy-store-blue">greater access</span> to <span class="blushing-salmon"> data</span> makes this universe <span class="golden">a better places to live</span></h2>

---

<img class="fullscreen-img" src="/presentations/img/city_hall.jpg" />

<h2>We make it <span class="toy-store-blue">easy</span> for <span class="blushing-salmon">organizations</span> to share their public data with <span class="golden">developers</span></h2>


===

# So what is an API anyway?

![APIs](../../img/Bubble_blue.tif.png)

---
<div style="text-align: left; font-size: 3em; line-height: 1.1em">
  <span class="blushing-salmon">A</span>pplication<br/>
  <span class="fragment" data-fragment-index=0><span class="toy-store-blue">P</span>rogramming<br/></span>
  <span class="fragment" data-fragment-index=1><span class="golden">I</span>nterface</span>
</div>

---

# Common Language

A <span class="blushing-salmon">consistent</span> way for <span class="toy-store-blue">two software systems</span> to <span class="golden">communicate</span>.

---

# Stable Platform

A <span class="blushing-salmon">guarantee</span> that the <span class="toy-store-blue">language</span> will not <span class="golden">change</span> without notice.
    
---

# Contract

An API is a <span class="blushing-salmon">contract</span> between a <span class="toy-store-blue">provider</span> and a <span class="golden">consumer</span>.

===

# Why are APIs important?

![APIs](../../img/Gear.png)

---

## Open data is messy

<pre>
C00000042|ILLINOIS TOOL WORKS FOR BETTER GOVERNMENT COMMITTEE|Michael J. Lynch|3600 W. Lake Avenue||Glenview|IL|60025|U|Q||Q|C|ILLINOIS TOOL WORKS INC|
C00000059|HALLMARK CARDS PAC|Swarens, Greg|2501 McGee|MD #288|Kansas City|MO|64108|U|Q|UNK|M|C|HALLMARK CARDS INCORPORATED|
C00000422|AMERICAN MEDICAL ASSOCIATION POLITICAL ACTION COMMITTEE|WALKER, KEVIN|25 MASSACHUSETTS AVENUE NW|SUITE 600|WASHINGTON|DC|20001|U|Q||M|M|AMERICAN MEDICAL ASSOCIATION|
C00000489|D R I V E POLITICAL FUND, CHAPTER 886|RON COBB|3528 WEST RENO||OKLAHOMA CITY|OK|73107|U|Q||Q|L|TEAMSTERS LOCAL UNION 886|
C00000547|KANSAS MEDICAL SOCIETY POLITICAL ACTION COMMITTEE|C. RICHARD BONEBRAKE, M.D.|623 SW 10TH AVE||TOPEKA|KS|66612|U|Q|UNK|Q|T|MEDICAL ASS'N; KANSAS          [AMPAC]|
C00000638|INDIANA STATE MEDICAL ASSOCIATION POLITICAL ACTION COMMITTEE|Kora, M.D., Vidya|322 Canal Walk, Canal Level|.|Indianapolis|IN|46202|U|Q||Q|M|Indiana State Medical Association|
C00000729|AMERICAN DENTAL POLITICAL ACTION CMTE.|Triftshauser, Roger W|1111 14th Street NW|Suite 1100|Washington|DC|20005|U|Q|UNK|M|T|DENTAL ASS'N; AMERICAN|
</pre>

Courtesy of <a href="ftp://ftp.fec.gov">ftp.fec.gov</a>
    
---
    
## A downloaded dataset is a stale dataset

![Clock](../../img/Alarm_clock.tif.png)

---

## Developers don’t want to manage custom datastores

![Hockey Puck](../../img/Database.tif.png)

---

## You want apps to be easily portable

![Rocket](../../img/Rocket.tif.png)

===

# The Socrata Open Data APIs

![SODA](../../img/can.png)

---

## Finding Data 
<br />
### [data.nasa.gov](https://data.nasa.gov/)
<br />
### [spaceappschallenge.org](https://2015.spaceappschallenge.org/challenge/)
Clean water mapping, forest monitor mapping, airburst data visualization,  transient watch challenges, and data treasure hunting
<br /><br />
### [dev.socrata.com/data](http://dev.socrata.com/data/)

---

## API Endpoints

Format:

<code>https://<span class="greenery">$domain</span>/<span class="toy-store-blue">resource</span>/<span class="golden">$identifier</span>.<span class="blushing-salmon">ext</span></code>

---

### In the Data Catalog

![API Sidebar](img/nasa-soda-sidebar.gif)

---

## Simple Filters

<code>http://data.nasa.gov/resource/b67r-rgxc.json?<code>
<code><span class="toy-store-blue">object_name</span>=<span class="golden">263P/Gibbs</span></code>

<pre><code data-trim contenteditable class="javascript">
[
  {
    "object": "263P/Gibbs",
    "object_name": "263P/Gibbs",
    "e": "0.5869803961",
    "w_deg": "26.31548584",
    "moid_au": "0.284398",
    "epoch_tdb": "54246",
    "q_au_2": "4.81",
    "q_au_1": "1.251302076",
    "tp_tdb": "2454098.266",
    "ref": "15",
    "p_yr": "5.27",
    "i_deg": "14.4711765",
    "node_deg": "113.3508576"
  }
]
</code></pre>

---

## SoQL Queries

<code>http://data.nasa.gov/resource/b67r-rgxc.json?<code>
<code>
<span class="toy-store-blue">$where</span>=<span class="golden">p_yr &lt; 5 AND epoch_tdb &gt; 55000</span>
</code>

<small style="padding-top: 5em">For more details see <a href="http://dev.socrata.com">dev.socrata.com</a></small>

---

## Aggregating Data

<code>http://data.nasa.gov/resource/b67r-rgxc.json?<code>
<code>
<span class="toy-store-blue">$select</span>=<span class="golden">e,count(e)</span><br/>&amp;<span class="toy-store-blue">$group</span>=<span class="golden">e</span><br/>&amp;<span class="toy-store-blue">$order</span>=<span class="golden">count_e DESC</span>
</code>

<pre><code data-trim contenteditable class="javascript">
[
  {
    "count_e": "7",
    "e": "0.6933582332"
  },
  {
    "count_e": "4",
    "e": "0.6824392137"
  },
  {
    "count_e": "2",
    "e": "0.6824329214"
  },
  {
    "count_e": "1",
    "e": "0.9671429085"
  }, ...
]
</code></pre>

---

## Paging Through Data

<code contenteditable>
/resource/abcd-1234.json?<br/>
<span class="toy-store-blue">$limit</span>=<span class="golden">50</span><br/>
&amp;<span class="toy-store-blue">$offset</span>=<span class="golden">100</span>
</code>

---

## Application Tokens

1. Register at [http://dev.socrata.com/register](http://dev.socrata.com/register)
2. Include as:
  - <code><span class="toy-store-blue">X-App-Token</span>: <span class="golden">$token</span></code> HTTP Header or ... 
  - The <code><span class="toy-store-blue">$$app_token</span>=<span class="golden">$token</span></code> URL parameter
3. Profit!!! (from more API requests)

===

# Help!

---

## Developer Portal

# [dev.socrata.com](http://dev.socrata.com)

<div class="footnote">Community powered! Learn how to <a href="http://dev.socrata.com/contributing.html">contribute</a>.</div>

--- 

## Getting Help

![Getting Help](/presentations/img/live-support.gif)

- In person
- IRC: [chat.freenode.net/#socrata-soda](irc://chat.freenode.net/#socrata-soda)
- Stack Overflow: [soda](http://stackoverflow.com/questions/tagged/soda) or [socrata](http://stackoverflow.com/questions/tagged/socrata)

---

## Libraries &amp; SDKs

<img src="../../img/socrata-heart-opensource.png"/>

### [dev.socrata.com/libraries/](http://dev.socrata.com/libraries/)

<div class="footnote"><a href="http://socrata.github.io/soda-ruby/">Ruby</a>, <a href="https://github.com/socrata/soda-scala">Scala</a>, <a href="http://socrata.github.io/soda-java/">Java</a>, <a href="https://github.com/socrata/soda-ios-sdk">ObjectiveC</a>, <a href="https://github.com/Chicago/RSocrata">R</a>, <a href="https://github.com/socrata/soda-swift">Swift</a>, etc.</div>

===

<img class="fullscreen-img" src="/presentations/img/team.jpg" />

## One more thing...

<h1 class="fragment" data-fragment-index="0">We're hiring!</h1>

<h2 class="fragment" data-fragment-index="1"><a href="http://www.socrata.com/careers">www.socrata.com/careers</a></h2>

===


<img class="fullscreen-img" src="/presentations/img/maggie.jpg"/>

# Thanks!

===

![Let's get this party started!](img/lets_get_this_party_started.gif)
