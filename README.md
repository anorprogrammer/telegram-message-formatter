<h2><a class="anchor" name="formatting-options" href="#formatting-options"><i class="anchor-icon"></i></a>Formatting options</h2>
<p>The Bot API supports basic formatting for messages. You can use bold, italic, underlined, strikethrough, and spoiler text, as well as inline links and pre-formatted code in your bots&#39; messages. Telegram clients will render them accordingly. You can use either markdown-style or HTML-style formatting.</p>
<p>Note that Telegram clients will display an <strong>alert</strong> to the user before opening an inline link (&#39;Open this link?&#39; together with the full URL).</p>
<p>Message entities can be nested, providing following restrictions are met:<br>- If two entities have common characters then one of them is fully contained inside another.<br>- <em>bold</em>, <em>italic</em>, <em>underline</em>, <em>strikethrough</em>, and <em>spoiler</em> entities can contain and can be part of any other entities, except <em>pre</em> and <em>code</em>.<br>- All other entities can&#39;t contain each other.</p>
<p>Links <code>tg://user?id=&lt;user_id&gt;</code> can be used to mention a user by their ID without using a username. Please note:</p>
<ul>
<li>These links will work <strong>only</strong> if they are used inside an inline link or in an inline keyboard button. For example, they will not work, when used in a message text.</li>
<li>These mentions are only guaranteed to work if the user has contacted the bot in the past, has sent a callback query to the bot via an inline button or is a member in the group where he was mentioned.</li>
</ul>
<h6><a class="anchor" name="markdownv2-style" href="#markdownv2-style"><i class="anchor-icon"></i></a>MarkdownV2 style</h6>
<p>To use this mode, pass <em>MarkdownV2</em> in the <em>parse_mode</em> field. Use the following syntax in your message:</p>
<pre><code>*bold \*text*
_italic \*text_
__underline__
~strikethrough~
||spoiler||
*bold _italic bold ~italic bold strikethrough ||italic bold strikethrough spoiler||~ __underline italic bold___ bold*
[inline URL](http://www.example.com/)
[inline mention of a user](tg://user?id=123456789)
`inline fixed-width code`
```
pre-formatted fixed-width code block
```
```python
pre-formatted fixed-width code block written in the Python programming language
```</code></pre>
<p>Please note:</p>
<ul>
<li>Any character with code between 1 and 126 inclusively can be escaped anywhere with a preceding &#39;\&#39; character, in which case it is treated as an ordinary character and not a part of the markup. This implies that &#39;\&#39; character usually must be escaped with a preceding &#39;\&#39; character.</li>
<li>Inside <code>pre</code> and <code>code</code> entities, all &#39;`&#39; and &#39;\&#39; characters must be escaped with a preceding &#39;\&#39; character.</li>
<li>Inside <code>(...)</code> part of inline link definition, all &#39;)&#39; and &#39;\&#39; must be escaped with a preceding &#39;\&#39; character.</li>
<li>In all other places characters &#39;_&#39;, &#39;*&#39;, &#39;[&#39;, &#39;]&#39;, &#39;(&#39;, &#39;)&#39;, &#39;~&#39;, &#39;`&#39;, &#39;&gt;&#39;, &#39;#&#39;, &#39;+&#39;, &#39;-&#39;, &#39;=&#39;, &#39;|&#39;, &#39;{&#39;, &#39;}&#39;, &#39;.&#39;, &#39;!&#39; must be escaped with the preceding character &#39;\&#39;.</li>
<li>In case of ambiguity between <code>italic</code> and <code>underline</code> entities <code>__</code> is always greadily treated from left to right as beginning or end of <code>underline</code> entity, so instead of <code>___italic underline___</code> use <code>___italic underline_\r__</code>, where <code>\r</code> is a character with code 13, which will be ignored.</li>
</ul>
<h6><a class="anchor" name="html-style" href="#html-style"><i class="anchor-icon"></i></a>HTML style</h6>
<p>To use this mode, pass <em>HTML</em> in the <em>parse_mode</em> field. The following tags are currently supported:</p>
<pre><code>&lt;b&gt;bold&lt;/b&gt;, &lt;strong&gt;bold&lt;/strong&gt;
&lt;i&gt;italic&lt;/i&gt;, &lt;em&gt;italic&lt;/em&gt;
&lt;u&gt;underline&lt;/u&gt;, &lt;ins&gt;underline&lt;/ins&gt;
&lt;s&gt;strikethrough&lt;/s&gt;, &lt;strike&gt;strikethrough&lt;/strike&gt;, &lt;del&gt;strikethrough&lt;/del&gt;
&lt;span class=&quot;tg-spoiler&quot;&gt;spoiler&lt;/span&gt;, &lt;tg-spoiler&gt;spoiler&lt;/tg-spoiler&gt;
&lt;b&gt;bold &lt;i&gt;italic bold &lt;s&gt;italic bold strikethrough &lt;span class=&quot;tg-spoiler&quot;&gt;italic bold strikethrough spoiler&lt;/span&gt;&lt;/s&gt; &lt;u&gt;underline italic bold&lt;/u&gt;&lt;/i&gt; bold&lt;/b&gt;
&lt;a href=&quot;http://www.example.com/&quot;&gt;inline URL&lt;/a&gt;
&lt;a href=&quot;tg://user?id=123456789&quot;&gt;inline mention of a user&lt;/a&gt;
&lt;code&gt;inline fixed-width code&lt;/code&gt;
&lt;pre&gt;pre-formatted fixed-width code block&lt;/pre&gt;
&lt;pre&gt;&lt;code class=&quot;language-python&quot;&gt;pre-formatted fixed-width code block written in the Python programming language&lt;/code&gt;&lt;/pre&gt;</code></pre>
<p>Please note:</p>
<ul>
<li>Only the tags mentioned above are currently supported.</li>
<li>All <code>&lt;</code>, <code>&gt;</code> and <code>&amp;</code> symbols that are not a part of a tag or an HTML entity must be replaced with the corresponding HTML entities (<code>&lt;</code> with <code>&amp;lt;</code>, <code>&gt;</code> with <code>&amp;gt;</code> and <code>&amp;</code> with <code>&amp;amp;</code>).</li>
<li>All numerical HTML entities are supported.</li>
<li>The API currently supports only the following named HTML entities: <code>&amp;lt;</code>, <code>&amp;gt;</code>, <code>&amp;amp;</code> and <code>&amp;quot;</code>.</li>
<li>Use nested <code>pre</code> and <code>code</code> tags, to define programming language for <code>pre</code> entity.</li>
<li>Programming language can&#39;t be specified for standalone <code>code</code> tags.</li>
</ul>
<h6><a class="anchor" name="markdown-style" href="#markdown-style"><i class="anchor-icon"></i></a>Markdown style</h6>
<p>This is a legacy mode, retained for backward compatibility. To use this mode, pass <em>Markdown</em> in the <em>parse_mode</em> field. Use the following syntax in your message:</p>
<pre><code>*bold text*
_italic text_
[inline URL](http://www.example.com/)
[inline mention of a user](tg://user?id=123456789)
`inline fixed-width code`
```
pre-formatted fixed-width code block
```
```python
pre-formatted fixed-width code block written in the Python programming language
```</code></pre>
<p>Please note:</p>
<ul>
<li>Entities must not be nested, use parse mode <a href="#markdownv2-style">MarkdownV2</a> instead.</li>
<li>There is no way to specify underline and strikethrough entities, use parse mode <a href="#markdownv2-style">MarkdownV2</a> instead.</li>
<li>To escape characters &#39;_&#39;, &#39;*&#39;, &#39;`&#39;, &#39;[&#39; outside of an entity, prepend the characters &#39;\&#39; before them.</li>
<li>Escaping inside entities is not allowed, so entity must be closed first and reopened again: use <code>_snake_\__case_</code> for italic <code>snake_case</code> and <code>*2*\**2=4*</code> for bold <code>2*2=4</code>.</li>
</ul>
