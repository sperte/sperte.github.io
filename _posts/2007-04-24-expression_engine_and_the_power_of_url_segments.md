---
title: ExpressionEngine and the Power of URL Segments
date: 2007-04-24
slug: expression_engine_and_the_power_of_url_segments
---
<p>I <a href="http://blog.virb.com/entries/blog-import-feature-is-live">had need</a> today to serve a separated RSS feed of just my blog articles &#8211; sans links and quick-posts. At first I thought I&#8217;d simply duplicate my RSS template and call it something like <code>rss-blog.php</code>.</p>

<p>Yeah right. Not with ExpressionEngine and its support for URL segment conditionals around. Ladies and gentlemen, pay attention, because this is all it took: <code>if segment_3 != 'blog'</code></p>

<p>Now, the when the URL is <code>http://seansperte.com/rss/blog</code> I can show unique content by placing it inside the <code>if</code> statement, like so:</p>

<ol class="code">
<li>weblog=&quot;blog1&#123;if segment_3 != &apos;blog&apos;&#125;|blog2&#123;/if&#125;&quot;</li>
</ol>

<p>See how that works? See how easy?</p>