Data Visualization with D3.js
==============================

By Igor Buinyi, igor.buinyi@gmail.com


Summary 
-------
I am visualizing the data from the two local elections to the Kyiv city council on May 25, 2014 and Oct 25, 2015. I focus on the results of Democratic Alliance party, for which the election of 2014 were the first in its history. For a fledging party, it is of critical importance to understand how to get support from the voters. Our visualization helps easily identify constituencies where the party activists perform the best in increasing the number of supporters.

Please find more information in layout_description.html



Design 
-------
I created this visualization to answer a real world question: Which candidates performed well during 2015 election campaign? (Note: The election systems were slightly different. In 2015 elections people voted for a particular candidate attached to their polling constituency. In 2014 elections they voted for the party in general, not for particular candidates.)  

It turns out that the absolute share of votes in the constituency is a bad measure of the candidate's efforts. For example, imagine candidate A who inherits a constituency with 6% support in 2014 and gets only 5% in 2015. His share of votes is higher than for candidate B who turns 1.5% support into 3.5%, but we should not say that candidate A performed better. Clearly, candidate B achieved a better dynamics in her constituency. Thus, I would like to identify *constituencies with the largest improvement in the share of votes achieved due to the candidate's effort.*

Of course, elections results are not deterministic and they follow a statistical distribution. The efforts might or might not pay off, or some candidates might be just lucky to have no strong opponents. But, on average, it is possible to identify constituencies where the candidates improved the results the most (or the least) due to their efforts.

The composition of elements on my chart was inspired by this example http://dimplejs.org/advanced_examples_viewer.html?id=advanced_storyboard_control. For the first version, I adapted the code from the link. I started to put on the chart y=[difference from the result expected by regression] and x=[the result expected by regression]. This setting clearly compares the effects introduced by different candidates.  But this chart was hard to understand even by those people who knew well about the election results before. 

In a response to the feedback I decided to depict y=[% in 2015] vs x=[% in 2014] ('results layout') which is a well understood layout. To guide viewers through the Martini glass, I put the green and red lines to separate areas of good/normal/bad performance and choose green/gray/red stroke for the corresponding circles. Good/bad performance is observed when the result in 2015 is at least 0.5 percentage points above/below the regression line. The rest is the normal performance. Then I added buttons for switching to the difference layout depicted in the first section. Due to animation, people easily understood how the difference layout was produced from the actual results. This change improved understanding a lot. 
The main takeaways from the chart are the following. First, in the results layout it is clearly seen that the level of support in different constituencies is very sticky, so that the earlier election is a good predictor for the current election results. Second, in the difference layout the chart allows identifying constituencies and candidates with good/bad performance.

Even though the final version inherits almost all the elements from the first version, I had to rewrite all code with D3.js to enhance the chart functionality. 

Other elements on the chart:
* Axes, axis ticks and axis titles: They are changed from the initial version.
* Legend: denotes constituencies with or without candidates, and with good or bad performance.
* Right menu: it is a functionality to show/hide data points for particular districts. The size of the buttons corresponds to the absolute number of votes for Democratic Alliance in the district. Buttons "Select All" and "Deselect All" allow to show/hide all data points at once.
* Tooltips: for data points on the main chart and district buttons in the right menu.
* Interaction: circles and buttons are highlighted when the pointer is over them; all circles for the districts are highlighted and stroke-width is increased to 2px when the pointer is over a district button.


Feedback
--------
First, I showed the initial version of the chart to 3 persons and noted their suggestions. Then I asked people to look at later versions.

Feedback to the first version:
**Person 1.** The tooltip information is hard to understand. He thought that only the points from particular district were shown (instead, all points were shown and constituencies from particular district were highlighted). He did not understand what "expected" share of votes meant. He suggested adding the functionality capable of showing/hiding the data from a district.

**Person 2.** She found that "Darnytskyi" button was highlighted after the chart was loaded. This is a bug, I did not intend to highlight anything upon the chart is loaded. Selection was needed only after the user clicked on a district button. She also suggested adding "All" button to manipulate points from all the districts. She did not understand well what the scales meant, both vertical and horizontal. She also said that blue fill color of circles and blue fill color for district buttons was confusing, so it was hard to understand what the blue color denoted.

**Person 3.** During our conversation we came to a conclusion that the chart lacks the Martini glass narrative. If I want to show good or bad performance, I have to highlight the corresponding circles deliberately. Also he suggested adding "Select All" and "Deselect All" buttons. 

It should be noted that nobody understood at first glance the different length of the district buttons. Later Person 2 suggested to arrange the buttons by the number of votes in the district (e.g. by the button length), instead of the alphabetical order.

So, my response was the following:
- change the basic layout to easily understandable y=[% in 2015] vs x=[% in 2014];
- denote good performance with green stroke and bad performance with red stroke and add green and red dashed lines;
- add buttons to switch to and from the 'difference layout';
- add animation for the transition between the layouts;
- the right menu allows to show/hide circles instead of highlight circles;
- add "Select All" and "Deselect All" buttons;
- arrange district buttons in the right menu according to their length;
- fine tune the tooltip text;
- rewrite axis titles and other text on the chart;
- add a few interaction elements (tooltips, opacity, highlighting) that allow the user to smoothly interact with the graph.

When I tested the functionality, I found a bug: when some circles are to be highlighted (for example, when the user moves the pointer over the buttons in the right menu), the circles stop moving even if the transition between layouts is not over. So I had to add a delay in case when the previous transition is still in progress. This improvement allows avoiding bugs when the user is too fast in interaction with the chart.


Resources
---------

**Dimple charts**
Layout examples
http://dimplejs.org/advanced_examples_viewer.html?id=advanced_storyboard_control
http://dimplejs.org/examples_viewer.html?id=bars_dual_measure_floating

Dimple documentation
https://github.com/PMSI-AlignAlytics/dimple/wiki/dimple.chart

Dimple tick format
http://stackoverflow.com/questions/22988109/dimple-js-measure-axis-values


**CSS**
Color scheme 
http://www.colorschemer.com/online.html

Gridlines (CSS styles)
http://bl.ocks.org/hunzy/11110940

Fonts 
https://developer.mozilla.org/en-US/docs/Web/CSS/font

Bootstrap (I do not include it in the submission, but I got inspired from it)
http://getbootstrap.com/css/


**D3.js**
D3 nested sums
http://bl.ocks.org/phoebebright/raw/3176159/

D3 axis labels 
http://stackoverflow.com/questions/11189284/d3-axis-labeling

D3 array 
https://github.com/mbostock/d3/wiki/Arrays

Hex to RGB
http://jsfiddle.net/ARTsinn/YSbwd/
http://stackoverflow.com/a/12342275/1250044
http://stackoverflow.com/a/6637537/1250044

Update axis using d3
http://stackoverflow.com/questions/16919280/how-to-update-axis-using-d3-js

Add line to a chart
http://stackoverflow.com/questions/29352970/dimple-js-add-vertical-line

Sort the dict
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort

Count the number of events in transition 
http://stackoverflow.com/questions/14024447/d3-js-transition-end-event

