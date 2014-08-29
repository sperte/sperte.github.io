---
title: 'Removing &#8220;www&#8221; From a Domain'
date: 2007-03-25
slug: removing_www_from_a_domain
---
<p>Here&#8217;s what I do to remove &#8220;www&#8221; from my domain. I put this code in my .htaccess file:</p>

<ol class="code">
 <li>RewriteEngine On</li>
 <li>#Handle removal of &#8220;www&#8221;</li>
 <li>RewriteCond %&#123;HTTP_HOST&#125; ^www.YOURDOMAIN.com(.*)$ [NC]</li>
 <li>RewriteRule ^(.*)$ http://YOURDOMAIN.com/$1 [R=301,L]</li>
</ol>

<p>A couple quick notes about this method if you want to use it as your own:</p>

<ol>
<li>In order to see/edit .htaccess, you may have to show &#8220;invisible&#8221; files in your FTP application.</li>
<li>This only works on servers running Apache.</li>
</ol>

<p>For more information, and a technical explanation of what each line does, <a href="http://daringfireball.net/2006/05/htaccess_redirection">read John Gruber&#8217;s post</a> (and subsequent opinion of why one would want to do this) from May 2006.</p>