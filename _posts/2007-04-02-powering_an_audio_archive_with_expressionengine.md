---
title: Powering an Audio Archive With ExpressionEngine
date: 2007-04-02
slug: powering_an_audio_archive_with_expressionengine
---
<p>One of the most often-asked questions I receive is about how <a href="http://thecity.org/audio">The City Church&#8217;s audio archive</a> is powered. It&#8217;s easier than you&#8217;d expect, but does require a bit of explanation. So, as promised, here&#8217;s a look under the hood.</p>

<h3>Custom fields and weblog preferences</h3>

<p>ExpressionEngine&#8217;s weblogs, or &#8220;databases&#8221; as I&#8217;ve labeled them, are much more flexible than a typical two- or three-field weblog. They can have custom fields, and have dozens of settings. I&#8217;ve assigned our Audio Archive database a custom field group which, beyond &#8220;title&#8221; and &#8220;URL title&#8221;, has <em>an additional 13 fields</em>. They include:</p>

<ul>
<li><code>subtitle</code></li>
<li><code>speaker</code> (a drop-down menu, pre-populated with our pastors&#8217; names)</li>
<li><code>speaker_alt</code> (a text field for the speaker name if it&#8217;s not listed in the drop-down)</li>
<li><code>campus</code></li>
<li><code>servicetime</code> (a drop-down menu)</li>
<li><code>servicetime_alt</code> (in case of an alternate service time)</li>
<li><code>summary</code></li>
<li><code>fileid</code></li>
<li><code>graphic</code></li>
<li><code>notes</code></li>
<li><code>keywords</code></li>
<li><code>scriptures</code></li>
</ul>

<p><img src="/assets/img/tccaa-fields.jpg" border="0" height="261" width="600" alt="Screenshot of the audio archive custom field group"  /></p>

<p>Each custom field comes with preference settings for type, formatting, hiding/showing, and instructions. Setting these preferences, I&#8217;m able to simplify the publish form as much as possible, but still give some advanced options to the publisher.</p>

<p>In addition to the custom fields, each entry (or &#8220;message&#8221; in this case) also has date, category, and status assignment(s). The nice thing about using a custom field for the service time is I don&#8217;t have to rely on our audio engineers (who do all the archive maintenance) to manually enter the service time in the entry date field &#8211; they simply click on the date itself. Also, since <span class="pullquote">entries can have multiple categories assigned to them</span>, a message can appear as a &#8220;Sunday Messages&#8221; and &#8220;Guest Speakers&#8221; entry simultaneously.</p>

<p>Speaking of categories, I&#8217;ve also set up a custom category group which has almost 30 categories (and sub-categories) for message assignment. They cover areas of ministry as well as special events. A few examples would be: &#8220;Sunday Messages&#8221;, &#8220;City Kids&#8221;, &#8220;Generation Church&#8221;, and &#8220;Men&#8217;s Ministry.&#8221;</p>

<p>The Audio Archive database also has some unique preferences that set it apart as a non-textual-based weblog. For instance, I&#8217;ve set the default status to be &#8220;closed&#8221; so that an entry can be created without it being immediately published and live. This enables an audio engineer to create the entry during a service while the message is being preached, but not have it available until he/she confirms the details of, say, the title or summary.</p>

<p>I&#8217;ve also set the database to: 1) disallow trackbacks (and auto-discovery code) in entries; 2) notify me via email of each entry published; 3) not show formatting buttons, author menu or forum topic on the publish page.</p>

<h3>Setting up the templates</h3>

<p>The fun stuff is in the templates. That&#8217;s where the magic happens. When displayed on a webpage, each message entry has links to listen, download, buy, etc.</p>

<p><img src="/assets/img/tccaa-styledmessage_20070401.jpg" border="0" height="63" width="506" alt="Screenshot of a styled message entry"  /></p>

<p>Here&#8217;s an example of a typical archive listing:</p>

<ol class="code">
    <li>&#123;exp:weblog:entries weblog=&quot;audioarchive&quot; limit=&quot;5&quot;&#125;</li>
    <li>&lt;div class=&quot;message&quot;&gt;</li>
    <li>&lt;p&gt;&lt;strong&gt;&lt;a href=&quot;&#123;url_title_path=message&#125;&quot;&gt;&#123;title&#125;&#123;if subtitle&#125; (&#123;subtitle&#125;)&#123;/if&#125;&lt;/a&gt;&lt;/strong&gt;&lt;br /&gt;</li>
    <li>&lt;span&gt;&#123;if speaker != &quot;other&quot;&#125;&#123;speaker&#125;&#123;if:else&#125;&#123;speaker_alt&#125;&#123;/if&#125;&lt;/span&gt; &#123;entry_date format=&quot;%M %j, %Y&quot;&#125; &amp;bull; &#123;if servicetime != &quot;other&quot;&#125;&#123;servicetime&#125;&#123;if:else&#125;&#123;servicetime_alt&#125;&#123;/if&#125; &amp;bull; &#123;campus&#125;&lt;/p&gt;</li>
    <li>&lt;ul&gt; </li>
    <li>&lt;li class=&quot;listen&quot;&gt;&lt;a href=&quot;/listen/&#123;entry_id&#125;&quot; onclick=&quot;NewWindow(this.href,&apos;Listen&apos;,&apos;400&apos;,&apos;150&apos;,&apos;no&apos;);return false&quot;&gt;Listen&lt;/a&gt;&lt;/li&gt;</li>
    <li>&lt;li class=&quot;download&quot;&gt;&lt;a href=&quot;/download.php?file=&#123;fileid&#125;.mp3&quot;&gt;Download&lt;/a&gt;&lt;/li&gt;</li>
    <li>&lt;li class=&quot;buy&quot;&gt;&lt;form name=&quot;post&quot; method=&quot;post&quot; action=&quot;http://www.ewebcart.com/cgi-bin/cart.pl&quot;&gt;</li>
    <li>&lt;!&#8211; shopping cart tags here //&#8211;&gt;</li>
    <li>&lt;a href=&quot;#&quot;&gt;&lt;input type=&quot;image&quot; src=&quot;http://www.thecity.org/images/spacer.gif&quot; width=&quot;16&quot; height=&quot;16&quot; name=&quot;add&quot; /&gt;&lt;/a&gt;</li>
    <li>&lt;/form&gt;&lt;/li&gt;</li>
    <li>&#123;if notes&#125;&lt;li class=&quot;notes&quot;&gt;&lt;a href=&quot;/pdf/&#123;notes&#125;&quot;&gt;Notes&lt;/a&gt;&lt;/li&gt;&#123;/if&#125;</li>
    <li>&lt;li class=&quot;comments&quot;&gt;&lt;a href=&quot;&#123;url_title_path=message&#125;&quot;&gt;&#123;if comment_total &gt;= &apos;2&apos;&#125;&#123;comment_total&#125; Comments&#123;if:elseif comment_total == &apos;1&apos;&#125;&#123;comment_total&#125; Comment&#123;if:else&#125;Add Comment&#123;/if&#125;&lt;/a&gt;&lt;/li&gt;</li>
    <li>&lt;/ul&gt;</li>
    <li>&lt;/div&gt;</li>
    <li>&#123;/exp:weblog:entries&#125;</li>
</ol>

<p>This code-block is found on the <a href="http://thecity.org/audio">index page</a> of the audio sub-section. Breaking it down, you can see I&#8217;ve wrapped each message in its own <code>div</code> with the class <code>message</code>. Inside the <code>div</code> I use a paragraph for <code>&#123;title&#125;</code> and some meta-info about the message. Notice the use of conditionals for <code>&#123;subtitle&#125;</code>, <code>speaker</code> and <code>servicetime</code>. If, for instance, the publisher gave the message a subtitle, it will appear in parenthesis after the title; if not, nothing will show.</p>

<p>Then (on line 5) comes the unordered list &#8211; with links to listen, download, buy, view notes or comment. The markup is pretty simple:</p>

<ul>
<li>For the <strong>listen</strong> link a JavaScript is used to open a new window and call a single-entry template (<code>/message/&#123;entry_id&#125;</code>). The single-entry template is basically just a few <abbr title="ExpressionEngine">EE</abbr> variables and an embedded MP3.</li>
<li>The <strong>download</strong> link utilizes <a href="http://elouai.com/force-download.php">a PHP script</a> that forces the users&#8217; browser to download the file (<code>&#123;fileid&#125;.mp3</code>) instead of load it.</li>
<li>The <strong>buy</strong> link is just a submit button inside a form with a bunch of ecommerce tags that pass the message data onto our third-party shopping cart app.</li>
<li>The <strong>notes</strong> link only appears if the &#123;notes&#125; field has a value.</li>
<li>The <strong>comments</strong> link uses a bunch of conditionals to either display the number of comments or &#8220;Add comment&#8221;.</li>
</ul>

<p><img src="/assets/img/tccaa-unstyledmessage.jpg" border="0" height="61" width="200" alt="Screenshot of an unstyled message entry" align="right" />When unstyled, this code-block is relatively plain and [arguably] semantic. The only point of contention comes from the use of a transparent GIF for the form submit button. In hindsight I suppose I could&#8217;ve just used <code>input type="image"</code>, but I was preoccupied in trying to utilize CSS for all images.</p>

<p>Of course, ExpressionEngine has built-in support for XML templates, so serving a podcast is just as simple:</p>

<ol class="code">
    <li>&#123;exp:weblog:entries weblog=&quot;audioarchive&quot; category=&quot;4&quot; orderby=&quot;date&quot; sticky=&quot;off&quot; limit=&quot;10&quot;  rdf=&quot;off&quot;&#125;</li>
    <li>&lt;item&gt;</li>
    <li>&lt;title&gt;&#123;exp:xml_encode&#125;&#123;title&#125;&#123;/exp:xml_encode&#125;&#123;if subtitle&#125; (&#123;exp:xml_encode&#125;&#123;subtitle&#125;&#123;/exp:xml_encode&#125;)&#123;/if&#125;&lt;/title&gt;</li>
    <li>&lt;link&gt;&#123;url_title_path=message&#125;&lt;/link&gt;</li>
    <li>&lt;guid isPermaLink=&quot;false&quot;&gt;&#123;fileid&#125;&lt;/guid&gt;</li>
    <li>&lt;description&gt;&lt;![CDATA[&#123;exp:markdown&#125;&#123;if summary&#125;&#123;summary&#125;&#123;if:else&#125;Speaker: &#123;if speaker_alt&#125;&#123;speaker_alt&#125;&#123;if:else&#125;&#123;speaker&#125;&#123;/if&#125; - This message was preached on &#123;entry_date format=&quot;%F %j%S&quot;&#125; at the &#123;servicetime&#125; service, at the &#123;campus&#125; Campus. No additional summary available.&#123;/if&#125;&#123;/exp:markdown&#125;]]&gt;&lt;/description&gt;</li>
    <li>&lt;dc:date&gt;&#123;entry_date format=&quot;%Y-%m-%d&quot;&#125;&lt;/dc:date&gt;</li>
    <li>&lt;!&#8211; itunes-specific item tags &#8211;&gt;</li>
    <li>&lt;itunes:author&gt;&#123;if speaker_alt !=&apos;&apos;&#125;&#123;speaker_alt&#125;&#123;/if&#125;&#123;if speaker_alt ==&apos;&apos;&#125;&#123;speaker&#125;&#123;/if&#125;&lt;/itunes:author&gt;</li>
    <li>&lt;itunes:subtitle&gt;&#123;if summary&#125;&#123;summary&#125;&#123;if:else&#125;Speaker: &#123;if speaker_alt&#125;&#123;speaker_alt&#125;&#123;if:else&#125;&#123;speaker&#125;&#123;/if&#125; - This message was preached on &#123;entry_date format=&quot;%F %j%S&quot;&#125; at the &#123;servicetime&#125; service, at the &#123;campus&#125; Campus. No additional summary available.&#123;/if&#125;&lt;/itunes:subtitle&gt;</li>
    <li>&lt;itunes:explicit&gt;no&lt;/itunes:explicit&gt;</li>
    <li>&#123;if keywords&#125;&lt;itunes:keywords&gt;&#123;keywords&#125;&lt;/itunes:keywords&gt;&#123;/if&#125;</li>
    <li>&lt;itunes:summary&gt;&#123;if summary&#125;&#123;summary&#125;&#123;if:else&#125;Speaker: &#123;if speaker_alt&#125;&#123;speaker_alt&#125;&#123;if:else&#125;&#123;speaker&#125;&#123;/if&#125; - This message was preached on &#123;entry_date format=&quot;%F %j%S&quot;&#125; at the &#123;servicetime&#125; service, at the &#123;campus&#125; Campus. No additional summary available.&#123;/if&#125;&lt;/itunes:summary&gt;</li>
    <li>&lt;!&#8211; end itunes-specific tags &#8211;&gt;</li>
    <li>&#123;exp:feed_enclosures&#125;&lt;a href=&quot;http://www.thecity.org/audioarchive/&#123;fileid&#125;.mp3&quot; rel=&quot;enclosure&quot;&gt;&#123;title&#125;&lt;/a&gt;&#123;/exp:feed_enclosures&#125;</li>
    <li>&lt;/item&gt;</li>
    <li>&#123;/exp:weblog:entries&#125;</li>
</ol>

<p>&#8230; Okay, so it doesn&#8217;t look so simple &#8211; but with proper code formatting and highlighting it becomes much easier to understand. I won&#8217;t go into detail about every line, but I will point out a few key elements.</p>

<p>First, notice the use of <code>&lt;![CDATA[ ... ]]&gt;</code> for the <code>&#123;summary&#125;</code> field. I use it because the field is set with no formatting, allowing me to format on the template-side &#8211; in this case, using the Markdown plugin.</p>

<p>Secondly, you can see I&#8217;m using a lot of iTunes-specific code. I suppose it goes without saying, but a podcast without these tags will have an uphill battle getting exposure on the iTunes Podcast Directory.</p>

<p>Finally, notice the actual file link is wrapped in <code>&#123;exp:feed_enclosures&#125;</code>. This tag performs some wizardry and somehow quantifies the file&#8217;s bit-size and serves a correctly formatted <code>enclosure</code> element. At least, I think that&#8217;s what it does.</p>

<h3>Maintaining the archives</h3>

<p>So with this infrastructure in place, <span class="pullquote">maintenance of the audio archive has been effortless for me</span>. The only thing I need to do is quality control; making sure message details are correct, no weird symbols are used, and the website stays online. I&#8217;m completely out of the loop during the process, which (I&#8217;ve been told) goes something like this:</p>

<ol>
<li>The message is recorded to a master CD during the service</li>
<li>The master CD is then ripped and (quickly) edited for content and equalization</li>
<li>The audio file is compressed and encoded as an MP3 (64k kbps, 22.050kHz, mono)</li>
<li>The file is uploaded to the server</li>
<li>A new entry is created in the audio archive <abbr title="ExpressionEngine">EE</abbr> database</li>
</ol>

<p>I&#8217;m yawning just thinking about how little I have to do to keep it all going. ExpressionEngine rocks.</p>