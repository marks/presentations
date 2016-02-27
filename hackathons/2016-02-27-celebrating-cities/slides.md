## <span class="title">Socrata Open Data APIs</span>
#### Celebrating Cities | Hack the Last Mile
![Socrata](img/snu_dev.png)

===

# Who the heck<br />are you?

![Socrata](/presentations/img/socrata-white-medium.png)

---

![Fullscreen](/presentations/img/at_table.jpg)

## We build _software_ to make data _more useful_ to _more people_

<!-- https://www.flickr.com/photos/hyku/2497370097 -->
--- 

![Fullscreen](/presentations/img/city.jpg)

<h2>We believe that _greater access_ to _public data_ makes the world a _better place to live_</h2>

---

![Fullscreen](/presentations/img/city_hall.jpg)

<h2>We make it _easy_ for _governments and non-profits_ to share their public data with _developers_</h2>

===

# The Socrata Open Data APIs

![SODA](../../img/can.png)

---

## Finding Data

### [celebratingcities.data.socrata.com](https://celebratingcities.data.socrata.com/)

![Socrata Open Data Portal search and results](img/celebratingcities.png)

---

## Finding More Data

### [opendatanetwork.com](https://www.opendatanetwork.com/)

![Open Data Network search and results](img/opendatanetwork.png)

---

### Getting to the good stuff (data)

![Data views](img/datadatadata.png)

---

### Getting to the better stuff (APIs)

![API Sidebar](http://dev.socrata.com/img/sidebar.gif)

---

## API Endpoints

<br />
<code style='font-size:120%;'>https://<span class="greenery">$domain</span>/resource/<span class="golden">$identifier</span>.<span class="blushing-salmon">$ext</span></code>

<br />

<p style='text-align: left; margin-left:50px;'><em>Where:</em></p>

- <code><span class="greenery">$domain</span></code> is the publisher's domain (ex: <code>celebratingcities.data.socrata.com</code>)
- <code><span class="golden">$identifier</span></code> is a dataset's unique ID (ex: <code>8qxj-ircv</code>)
- <code><span class="blushing-salmon">$ext</span></code> is <code>json</code>, <code>geojson</code>, <code>csv</code>, <code>xml</code>, or <code>rdf</code>

---

### Example: Head Start Locations

<a target='blank' style='color:#FFF !important' href='https://celebratingcities.data.socrata.com/resource/8qxj-ircv.json'><code style=''>https://<span class="greenery">celebratingcities.data.socrata.com</span><br />/resource/<span class="golden">8qxj-ircv</span>.<span class="blushing-salmon">json</span></code></a>

<pre>
  <code data-trim contenteditable class="javascript">
[
  { // first result
    "name": "Big Mama's",
    "centertype": "Early Head Start",
    "delegateno": "200",
    "grantnumbe": "03HP0017",
    "location": {
    "type": "Point",
      "coordinates": [ -77.010447, 38.821247 ]
    },
    "location_address": "4680 Martin Luther King Jr Ave SW",
    "location_city": "Washington",
    "location_state": "DC",
    "location_zip": "20032-1132",
    "programadd": "810 First Street, NE 9th Floor",
    "programcit": "Washington",
    "programdel": "Office of the State Superintendent of Education",
    "programsta": "DC",
    "programtyp": "Early Head Start",
    "programzip": "20002-4227",
    "grantee": "Office of the State Superintendent of Education\n810 First Street, NE\n9th Floor\nWashington, DC 20002-4227\n(202)741-7632 - \n"
  }, // ... more results ...
]
  </code>
</pre>


---

## Simple Filters

<a target='blank' style='color:#FFF !important' href='https://celebratingcities.data.socrata.com/resource/8qxj-ircv.json?centertype=Migrant+and+Seasonal+Head+Start'><code style=''>https://<span class="greenery">celebratingcities.data.socrata.com</span><br />/resource/<span class="golden">8qxj-ircv</span>.<span class="blushing-salmon">json</span>
<br />?<span class="toy-store-blue">centertype</span>=<span style="color:MediumOrchid">Migrant+and+Seasonal+Head+Start
</code></a>

<pre><code data-trim contenteditable class="javascript">
[
  {
    "name": "Parksley Migrant Head Start",
    "centertype": "Migrant and Seasonal Head Start",
    "delegateno": "1",
    "grantnumbe": "90CM9796",
    "location": {
      "type": "Point",
      "coordinates": [ -75.604929, 37.789462 ]
    },
    "location_address": "20344 Lankford Hwy P.O. Box 497",
    "location_city": "Parksley",
    "location_state": "VA",
    "location_zip": "23421-3746",
    "phone": "(757) 665-4976",
    "programadd": "1214 West Graham Road, Suite 3",
    "programcit": "Richmond",
    "programdel": "Rural Family Development",
    "programsta": "VA",
    "programtyp": "Migrant and Seasonal Head Start",
    "programzip": "23220-1400",
    "grantee": "Rural Family Development\n1214 West Graham Road, Suite 3\nRichmond, VA 23220-1400\n(757)709-4817 - \n"
  }, // ... more results ...
]
</code></pre>

---

## SoQL Queries

<a href='https://celebratingcities.data.socrata.com/resource/8qxj-ircv.json?$where=programsta%20IN%20(%27DC%27,%27MD%27)'>

<a target='blank' style='color:#FFF !important' href='https://celebratingcities.data.socrata.com/resource/8qxj-ircv.json?$where=programsta%20IN%20(%27DC%27,%27MD%27)%20AND%20delegateno%20BETWEEN%200%20and%20200'><code style=''>https://<span class="greenery">celebratingcities.data.socrata.com</span><br />/resource/<span class="golden">8qxj-ircv</span>.<span class="blushing-salmon">json</span>?<span class="toy-store-blue">$where=</span>
<br /><br /></span>programsta IN ('DC','MD')<br />AND<br />delegateno BETWEEN 0 and 200
</code></a>

<small style="padding-top: 5em">For more details see <a href="http://dev.socrata.com">dev.socrata.com</a></small>

---

## Aggregating Data

<a target='blank' style='color:#FFF !important' href='https://celebratingcities.data.socrata.com/resource/8qxj-ircv.json?$select=programtyp,count(*)&$group=programtyp&$order=count%20desc'><code style=''>https://<span class="greenery">celebratingcities.data.socrata.com</span><br />/resource/<span class="golden">8qxj-ircv</span>.<span class="blushing-salmon">json</span>?<span class="toy-store-blue">$select</span>=<span style="color:MediumOrchid">programtyp,count(*)</span>
<br />
&<span class="toy-store-blue">$group</span>=<span style="color:MediumOrchid">programtyp</span>&<span class="toy-store-blue">$order</span>=<span style="color:MediumOrchid">count desc</span></span>
</code></a>

<pre><code data-trim contenteditable class="javascript">
[
  {
    "count": "701",
    "programtyp": "Head Start"
  },
  {
    "count": "166",
    "programtyp": "Early Head Start"
  },
  {
    "count": "2",
    "programtyp": "Migrant and Seasonal Head Start"
  }
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
  - `X-App-Token: $token` HTTP Header or ... 
  - The `$$app_token = $token` URL parameter
3. Hack the last mile!

===

# Help!

---

## Developer Portal

# [dev.socrata.com](http://dev.socrata.com)

<div class="footnote">Community powered! Learn how to <a href="http://dev.socrata.com/contributing.html">contribute</a>.</div>

---

## Libraries &amp; SDKs

<img src="../../img/socrata-heart-opensource.png"/>

### [dev.socrata.com/libraries/](http://dev.socrata.com/libraries/)

<div class="footnote"><a href="http://socrata.github.io/soda-ruby/">Ruby</a>, <a href="https://github.com/socrata/soda-scala">Scala</a>, <a href="http://socrata.github.io/soda-java/">Java</a>, <a href="https://github.com/socrata/soda-ios-sdk">ObjectiveC</a>, <a href="https://github.com/Chicago/RSocrata">R</a>, <a href="https://github.com/socrata/soda-swift">Swift</a>, etc.</div>

--- 

## Getting Help

![Getting Help](/presentations/img/live-support.gif)

- Track me down!
- IRC: [chat.freenode.net/#socrata-soda](irc://chat.freenode.net/#socrata-soda)
- Stack Overflow: [soda](http://stackoverflow.com/questions/tagged/soda) or [socrata](http://stackoverflow.com/questions/tagged/socrata)


===

![Fullscreen](/presentations/img/work_tounge.gif)

## One more thing...

<h1 class="fragment" data-fragment-index="0">We're hiring!</h1>

<h2 class="fragment" data-fragment-index="1"><a href="http://careers.socrata.com">careers.socrata.com</a></h2>

===

![Let's get this party started!](/presentations/img/lets_get_this_party_started.gif)

===

<img class="fullscreen-img" src="/presentations/img/team.jpg"/>

# Thanks!

