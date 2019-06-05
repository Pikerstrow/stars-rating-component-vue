<h2>Description</h2>
<p>
Simple star rating component made on Vue.js with a bunch of options and ability to set rating with half star.
</p>

<h2>Screen Shots</h2>
<p><img src="https://user-images.githubusercontent.com/39648888/58760255-1f3bf380-853e-11e9-9f08-48189ee87345.png"></p>

<h2>Features</h2>
<ul>
<li>Stars are SVG elements</li>
<li>Customizable number of stars</li>
<li>Stars can be substituted by other elements</li>
<li>Each star is divided on two halves (there is ability to set a 3.5 rating for example)</li>
<li>Customizable color, size, space between stars, color on hover, color on select, color of stroke and stroke width.</li>
<li>Read only option'</li>
</ul>

<h2>Demo</h2>
<p>Live demo - <a href="http://demo-stars-rating.web-ol-mi.pp.ua/">http://demo-stars-rating.web-ol-mi.pp.ua/</a></p>

<h2>Installation</h2>
<p><pre>$npm install stars-rating-component-vue --save</pre></p>

<h2>Usage</h2>
<p>After installation, all you need is import component, using the next syntax:</p>
<pre>import StarsRating from "stars-rating-component-vue"</pre>
<p>and bind needed property with the component using "v-model".</p>

<h2>Options and configurations</h2>
<p>If you want to change default options, you need to pass <b>object</b> with own desired options/settings to the component using "v-bind" (example of options object is further)</p>

<b>a) example of usage without options (default ones)</b>
<p><img src="https://user-images.githubusercontent.com/39648888/58760631-4a751180-8543-11e9-9e15-a34d2b31de56.png"></p>

<b>a) example of usage with options</b>
<p><img src="https://user-images.githubusercontent.com/39648888/58760431-527f8200-8540-11e9-9870-973d184e310b.png"></p>

<h4>Available configurations</h4>
<table>
    <thead>
        <tr>
            <th>Property</th>
            <th>Data type</th>
            <th>Details</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>starsQuantity</td>
            <td>number</td>
            <td>Property sets number of stars for rating.</td>
        </tr>
        <tr>
            <td>stroke</td>
            <td>string</td>
            <td>Property sets color of stars stroke. Accepts any valid CSS-color</td>
        </tr>
        <tr>            
            <td>strokeWidth</td>
            <td>number</td>
            <td>Property sets width of stars stroke. Accepts number</td>
        </tr>
        <tr>
            <td>fill</td>
            <td>string</td>
            <td>Property sets color of stars. Accepts any valid CSS-color</td>
        </tr>
        <tr>
            <td>highlighted</td>
            <td>string</td>
            <td>Property sets color of selected stars. Accepts any valid CSS-color</td>
        </tr>
        <tr>
            <td>hover</td>
            <td>string</td>
            <td>Property sets color of hovered stars. Accepts any valid CSS-color</td>
        </tr>
        <tr>
            <td>size</td>
            <td>number</td>
            <td>Property sets size of stars. Accepts number, which will be used for setting width of stars in px</td>
        </tr>
        <tr>
            <td>marginRight</td>
            <td>number</td>
            <td>Property sets space between stars. Accepts number, which will be used for setting 'margin-right' option in px</td>
        </tr>
        <tr>
            <td>readOnly</td>
            <td>boolean</td>
            <td>Property enables or disables ability to set rating</td>
        </tr>
        <tr>
            <td>rating</td>
            <td>number</td>
            <td>If readOnly is true, this property will be used for showing correct rating</td>
        </tr>
        <tr>
            <td>d</td>
            <td>string</td>
            <td>Using this property you can change default stars for any other elements! This property is 'd' attribute of SVG 'path' element. You can read more about it on <a href="https://developer.mozilla.org/en-US/docs/Web/SVG/Attribute/d">MDN</a>. <b>Important!</b> For correct replacing of the default stars, you ned to also set 'viewBox' property... </td>
        </tr>
        <tr>
            <td>viewBox</td>
            <td>string</td>
            <td>Another property which allows to change the default stars for any other elements...</td>
        </tr>
    </tbody>
</table>


<h4>Default configuration</h4>
<table>
    <thead>
        <tr>
            <th>Property</th>
            <th>Value</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>starsQuantity</td>
            <td>5</td>
        </tr>
        <tr>
            <td>stroke</td>
            <td>'none'</td>
        </tr>
        <tr>            
            <td>strokeWidth</td>
            <td>0</td>
        </tr>
        <tr>
            <td>fill</td>
            <td>'#DDD'</td>
        </tr>
        <tr>
            <td>highlighted</td>
            <td>'#FFDF12'</td>
        </tr>
        <tr>
            <td>hover</td>
            <td>'#FFED84'</td>
        </tr>
        <tr>
            <td>size</td>
            <td>25</td>
        </tr>
        <tr>
            <td>marginRight</td>
            <td>5</td>
        </tr>
        <tr>
            <td>readOnly</td>
            <td>false</td>
        </tr>
        <tr>
            <td>rating</td>
            <td>0</td>
        </tr>
        <tr>
            <td>d</td>
            <td>M50 0 l-15 35 -35 5 25 24 -6 35 31 -18 31 18 -6 -35 25 -24 -35 -5 -15 -35 z</td>
        </tr>
        <tr>
            <td>viewBox</td>
            <td>0 0 100 100</td>
        </tr>
    </tbody>
</table>

<h4>Example of Options object:</h4>
<pre>
    options: {
        starsQuantity: 5,
        stroke: 'none',
        strokeWidth: 0,
        fill: '#DDD',
        highlighted: '#FFDF12',
        hover: '#FFED84',
        size: 25,
        readOnly: false,
        rating: 0,
        marginRight: 5,
        d: "M50 0 l-15 35 -35 5 25 24 -6 35 31 -18 31 18 -6 -35 25 -24 -35 -5 -15 -35 z",
        viewBox: "0 0 100 100"
    }
</pre>

<h2>License</h2>
<p>License: <b>MIT</b>. You are free to use it without any restrictions. But I would very appreciate if you send me an email (oleksandrmischuk@gmail.com) with the name of your country and city/town/village :) </p>


