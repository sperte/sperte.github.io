---
title: Go Broncos (and/or Seahawks)
date: 2006-01-19
slug: team_badges
---
<p>In honor of the Divisional Championships this weekend, I&#8217;ve whipped up some support badges for you to steal and use on your website. They come in two variations, the two teams I&#8217;ll actually be rooting for: Broncos and Seahawks.</p>

<p><a href="http://www.seansperte.com/images/broncos_badge.png">Broncos badge</a></p>

<p><a href="http://www.seansperte.com/images/seahawks_badge.png">Seahawks badge</a></p>

<p>(Please don&#8217;t link directly to those files &#8211; I don&#8217;t want to have to pull them off my host or block external bandwidth mooching.)</p>

<p>The markup is quite simple:</p>

<pre><code>&lt;p id="broncos"&gt;&lt;a href="http://www.denverbroncos.com/"&gt;Go Broncos&lt;/a&gt;&lt;/p&gt;
</code></pre>

<p>And the CSS is:</p>

<pre><code>
#broncos &#123;
    position: fixed;
    top: 0;
    left: 0;
    width: 190px;
    margin: 0;
    &#125;
#broncos a &#123;
    display: block;
    height: 110px;
    text-decoration: none;
    text-indent: -5000px;
    overflow: hidden;
    background: url(/images/broncos_badge.png) no-repeat;
    &#125;
</code></pre>

<p>Since these are .png images, you may want to use some <a href="http://allinthehead.com/retro/69/sleight-of-hand">JavaScript magic</a> to load Microsoft&#8217;s PNG support, or else IE/5-6 will show a greyish box behind the image. (Also note, once the alpha has been loaded by IE, the link no longer works.)</p>

<p>Have fun, and <strong>go Broncos!</strong></p>