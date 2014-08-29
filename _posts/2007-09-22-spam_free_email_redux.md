---
title: Spam Free Email Redux
date: 2007-09-22
slug: spam_free_email_redux
---
<p><a href="http://www.masugadesign.com">Ryan Masuga</a> emailed me with a great question about my spam-free email setup:</p>

<blockquote>
  <p>if I wanted to change my private email address a couple months down the line [&#8230;] what would happen to any mailboxes I made for the private1234@ address?</p>
</blockquote>

<p>I didn&#8217;t have a good answer for him since I don&#8217;t store my email in boxes or the inbox; instead, I use <a href="http://www.43folders.com/izero/">Merlin Mann&#8217;s Inbox Zero</a> methodology, plus a folder in my home directory where I save all archived emails.</p>

<p>Ryan did some research and found his answer:</p>

<blockquote>
  <p>I found that reducing the number of folders I have made things pretty easy, but isn&#8217;t really necessary either. All you need to do is ftp into your site to be able to see the &#8216;home/&#123;youracct&#125;/mail/&#123;yourdomain&#125;/&#8217; directory (I think&#8230;) and within that directory are your mail accounts. Copy mailboxes (I&#8217;m on Apache) from old private email directory to the new private email directory and voila - you&#8217;ve just moved all the mailboxes. You could probably scp these as well, but I&#8217;m not that technically savvy and just copying via Transmit seemed to work OK.</p>
</blockquote>

<p>Easy enough &#8211; if you have access to your server mail directories.</p>