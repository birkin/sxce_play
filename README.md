Goal here, trying to get an html page to display the result of two things:
- a source data file that uses an xinclude
- a stylesheet transformation on the source data file (after the xinclude is processed)

There's practically no display output in 'output.html'.

What's _supposed_ to happen is that when viewing 'output.html' in a browser:

    First, 'data.xml', which natively contains data about the 'Empire Burlesque' CD, sucks in (via xinclude) the data about the 'Hide your heart' CD in 'include.xml'. At this point, 'data.xml' could be thought to contain data about both CDs.

    Then, the _two_ CDs from 'data.xml' are tranformed into html using 'stylesheet.xsl'.

At this point, only the native Empire Burlesque CD is displayed, indicating that saxon-ce is performing the transform, but that the x-include is not working.

To be continued...
