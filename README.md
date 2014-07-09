### goal

Goal here, trying to get an html page to display the result of two things:
- a source data file that uses an xinclude
- a stylesheet transformation on the source data file (after the xinclude is processed)

There's practically no display output in 'output.html'.

What's _supposed_ to happen is that when viewing 'output.html' in a browser:

- First, 'data.xml', which natively contains data about the 'Empire Burlesque' CD, sucks in (via xinclude) the data about the 'Hide your heart' CD in 'include.xml'. At this point, 'data.xml' could be thought to contain data about both CDs.

- Then, the _two_ CDs from 'data.xml' are tranformed into html using 'stylesheet.xsl'.

At this point, only the native Empire Burlesque CD is displayed, indicating that saxon-ce is performing the transform, but that the xinclude is not working.

---

### oxygen gets it right

To see the intended result...
- I loaded 'data.xml' in oxygen
- selected menus Document -> Transformation -> Configure Transformation Scenario
- selected button New -> XML transformation with XSLT
- in dialog box...
    - (current file already selected in 'XML URL')
    - selected via folder the 'XSL URL' path to 'stylesheet.xsl'
    - selected the 'Saxon-HE 9.5.1.2' Transformer (at oxygen's suggestion from a previous unsuccessful transform attempt)
- selected the 'Apply Associated' button -- and got the xml saved as `oxygen_transform.html`

[oxygen_transform.png][screenshot_link] is a screenshot of that html from Safari.

---

### plan of attack

E.M. says one approach that should work is to have saxon-ce first apply an 'xi:include processor', [xipr.xsl][github_xipr_link], and _then_ apply the regular stylesheet.

---

### no saxon-ce success yet, but oxygen again gets it right

- I got the 'low-level' approach for the basic saxon-ce transform working (xinclude not working), thinking this might help in future work: see `output_b.html`

- I added the xipr xsl file to the project

- I tried transforming it using the low-level approach (`output_c.html`) -- didn't initially see any output, and switched gears to see if I could apply the xipr stylesheet using oxygen, using the steps listed above ('oxygen gets it right').

- That worked; producing valid new source xml (output saved to `oxygen_transform_with_xipr.xml`). I then used oxygen to transform that new source xml with stylesheet.xsl, which worked.

- So I need to get saxon-ce to correctly apply the xipr xsl. Investigating further....

---

### resources

- [saxon-ce docs](http://www.saxonica.com/ce/user-doc/1.1/html/starting/running/)

To be continued...

TODO: document output_d.html


[screenshot_link]: https://github.com/birkin/sxce_play/blob/master/oxygen_transform.png
[github_xipr_link]: https://github.com/dret/XIPr
