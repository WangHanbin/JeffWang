<h3 id="im-hanbin-wang">I’m Hanbin Wang</h3>

<p><div class="toc"><div class="toc">
<ul>
<li><ul>
<li><ul>
<li><a href="#im-hanbin-wang">I’m Hanbin Wang</a></li>
<li><a href="#the-power-of-algorithms">The Power of Algorithms</a></li>
<li><a href="#graph-algorithms">Graph Algorithms</a></li>
<li><a href="#markdown-is-not-that-hard">Markdown is not that hard!</a><ul>
<li><a href="#introduction">Introduction</a></li>
<li><a href="#some-basic-syntaxes">Some Basic Syntaxes</a></li>
<li><a href="#online-resources">Online Resources</a></li>
</ul>
</li>
<li><a href="#tts">TTS</a></li>
</ul>
</li>
</ul>
</li>
</ul>
</div>
</div>
</p>

<p><a></a></p>



<h3 id="the-power-of-algorithms">The Power of Algorithms</h3>

<p><strong>Algorithms came to rule our world</strong> <br>
Why I want to post something about algorithms here?    </p>

<blockquote>
  <ul>
  <li>Write some blogs about computer science</li>
  <li>Output is very important</li>
  <li>Share my ideas with others</li>
  </ul>
</blockquote>

<p><strong>Genius is nothing more nor less than childhood recaptured at will.</strong> <br>
 <strong>Although I am not a genius, I have the eager desire to learn.</strong> <br>
<a></a></p>



<h3 id="graph-algorithms">Graph Algorithms</h3>

<ul>
<li><a href="http://blog.csdn.net/whb923/article/details/42522331">Single Source Shortest Path</a></li>
<li><a href="http://blog.csdn.net/whb923/article/details/42915213">Dijkstra’s Shortest-Path Algorithm Implementation</a></li>
</ul>

<p><a></a></p>



<h3 id="markdown-is-not-that-hard">Markdown <strong><em>is not</em></strong> that hard!</h3>



<h4 id="introduction">Introduction</h4>

<p>I found an <em>online tutorial</em>, <br>
I will complete these lessons to learn how to use <strong>Markdown</strong>.</p>

<p>By the way, I like NAO!! <br>
 <img src="http://upload.wikimedia.org/wikipedia/commons/thumb/c/cf/NAO-Robot.jpg/270px-NAO-Robot.jpg" alt="picture" title=""></p>



<h4 id="some-basic-syntaxes">Some Basic Syntaxes</h4>

<blockquote>
  <ul>
  <li><strong>Bold</strong> (” <em>* *</em> <em>* *</em> “)</li>
  <li><em>Italic</em> (“_ _” )</li>
  <li>Header (####)</li>
  <li>Link  inline link (<em>[ ] ( )</em>)&amp; reference link([ ] [ ]; [ ]:link )</li>
  <li>Insert a Picture (Use exclamation point <strong>“!”</strong>) </li>
  <li>Block Quote(Use “greater than” &gt;)</li>
  <li>Lists  <br>
  <ul><li>Ordered (1. 2. 3. )</li>
  <li>Unordered( ” * ” )</li>
  <li>Nest</li></ul></li>
  <li>Formatting paragraphs <br>
  <ol><li>Soft Break: inserting two spaces <em>after</em> each new line </li>
  <li>Hard Break:  insert a new line forcefully, press <em>“Enter”</em></li></ol></li>
  </ul>
</blockquote>



<h4 id="online-resources">Online Resources</h4>

<ul>
<li><a href="http://en.wikipedia.org/wiki/Markdown#Syntax_examples"><strong>Wikipedia about Markdown Syntax</strong></a></li>
<li><a href="https://stackedit.io/editor"><strong>StackEdit– In-browser Markdown Editor</strong></a></li>
<li><a href="http://marxi.co/#introducing-markdown"><strong>Marxico–Markdown Editor for Evernote</strong></a></li>
<li><a href="https://help.github.com/articles/writing-on-github/"><strong>Writing on Github</strong></a></li>
<li><a href="https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet#links"><strong>Markdown Cheatsheet</strong></a></li>
</ul>



<h3 id="tts">TTS</h3>



<pre class="prettyprint"><code class="language-python hljs "><span class="hljs-comment">#!/usr/bin/python</span>

<span class="hljs-keyword">import</span> sys
<span class="hljs-keyword">import</span> argparse
<span class="hljs-keyword">import</span> re
<span class="hljs-keyword">import</span> urllib, urllib2
<span class="hljs-keyword">import</span> time
<span class="hljs-keyword">from</span> collections <span class="hljs-keyword">import</span> namedtuple


<span class="hljs-function"><span class="hljs-keyword">def</span> <span class="hljs-title">split_text</span><span class="hljs-params">(input_text, max_length=<span class="hljs-number">100</span>)</span>:</span>
    <span class="hljs-string">"""
    Try to split between sentences to avoid interruptions mid-sentence.
    Failing that, split between words.
    See split_text_rec
    """</span>
    <span class="hljs-function"><span class="hljs-keyword">def</span> <span class="hljs-title">split_text_rec</span><span class="hljs-params">(input_text, regexps, max_length=max_length)</span>:</span>
        <span class="hljs-string">"""
        Split a string into substrings which are at most max_length.
        Tries to make each substring as big as possible without exceeding
        max_length.
        Will use the first regexp in regexps to split the input into
        substrings.
        If it it impossible to make all the segments less or equal than
        max_length with a regexp then the next regexp in regexps will be used
        to split those into subsegments.
        If there are still substrings who are too big after all regexps have
        been used then the substrings, those will be split at max_length.
        Args:
            input_text: The text to split.
            regexps: A list of regexps.
                If you want the separator to be included in the substrings you
                can add parenthesis around the regular expression to create a
                group. Eg.: '[ab]' -&gt; '([ab])'
        Returns:
            a list of strings of maximum max_length length.
        """</span>
        <span class="hljs-keyword">if</span>(len(input_text) &lt;= max_length): <span class="hljs-keyword">return</span> [input_text]

        <span class="hljs-comment">#mistakenly passed a string instead of a list</span>
        <span class="hljs-keyword">if</span> isinstance(regexps, basestring): regexps = [regexps]
        regexp = regexps.pop(<span class="hljs-number">0</span>) <span class="hljs-keyword">if</span> regexps <span class="hljs-keyword">else</span> <span class="hljs-string">'(.{%d})'</span> % max_length

        text_list = re.split(regexp, input_text)
        combined_text = []
        <span class="hljs-comment">#first segment could be &gt;max_length</span>
        combined_text.extend(split_text_rec(text_list.pop(<span class="hljs-number">0</span>), regexps, max_length))
        <span class="hljs-keyword">for</span> val <span class="hljs-keyword">in</span> text_list:
            current = combined_text.pop()
            concat = current + val
            <span class="hljs-keyword">if</span>(len(concat) &lt;= max_length):
                combined_text.append(concat)
            <span class="hljs-keyword">else</span>:
                combined_text.append(current)
                <span class="hljs-comment">#val could be &gt;max_length</span>
                combined_text.extend(split_text_rec(val, regexps, max_length))
        <span class="hljs-keyword">return</span> combined_text

    <span class="hljs-keyword">return</span> split_text_rec(input_text.replace(<span class="hljs-string">'\n'</span>, <span class="hljs-string">''</span>),
                          [<span class="hljs-string">'([\,|\.|;]+)'</span>, <span class="hljs-string">'( )'</span>])


audio_args = namedtuple(<span class="hljs-string">'audio_args'</span>,[<span class="hljs-string">'language'</span>,<span class="hljs-string">'output'</span>])

<span class="hljs-function"><span class="hljs-keyword">def</span> <span class="hljs-title">audio_extract</span><span class="hljs-params">(input_text=<span class="hljs-string">''</span>,args=None)</span>:</span>
    <span class="hljs-comment"># This accepts :</span>
    <span class="hljs-comment">#   a dict,</span>
    <span class="hljs-comment">#   an audio_args named tuple</span>
    <span class="hljs-comment">#   or arg parse object</span>
    <span class="hljs-keyword">if</span> args <span class="hljs-keyword">is</span> <span class="hljs-keyword">None</span>:
        args = audio_args(language=<span class="hljs-string">'en'</span>,output=open(<span class="hljs-string">'output.mp3'</span>, <span class="hljs-string">'w'</span>))
    <span class="hljs-keyword">if</span> type(args) <span class="hljs-keyword">is</span> dict:
        args = audio_args(
                    language=args.get(<span class="hljs-string">'language'</span>,<span class="hljs-string">'en'</span>),
                    output=open(args.get(<span class="hljs-string">'output'</span>,<span class="hljs-string">'output.mp3'</span>), <span class="hljs-string">'w'</span>)
        )
    <span class="hljs-comment">#process input_text into chunks</span>
    <span class="hljs-comment">#Google TTS only accepts up to (and including) 100 characters long texts.</span>
    <span class="hljs-comment">#Split the text in segments of maximum 100 characters long.</span>
    combined_text = split_text(input_text)

    <span class="hljs-comment">#download chunks and write them to the output file</span>
    <span class="hljs-keyword">for</span> idx, val <span class="hljs-keyword">in</span> enumerate(combined_text):
        mp3url = <span class="hljs-string">"http://translate.google.com/translate_tts?tl=%s&amp;q=%s&amp;total=%s&amp;idx=%s"</span> % (
            args.language,
            urllib.quote(val),
            len(combined_text),
            idx)
        headers = {<span class="hljs-string">"Host"</span>: <span class="hljs-string">"translate.google.com"</span>,
                   <span class="hljs-string">"Referer"</span>: <span class="hljs-string">"http://www.gstatic.com/translate/sound_player2.swf"</span>,
                   <span class="hljs-string">"User-Agent"</span>: <span class="hljs-string">"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_7_3) "</span>
                                 <span class="hljs-string">"AppleWebKit/535.19 (KHTML, like Gecko) "</span>
                                 <span class="hljs-string">"Chrome/18.0.1025.163 Safari/535.19"</span>
        }
        req = urllib2.Request(mp3url, <span class="hljs-string">''</span>, headers)
        sys.stdout.write(<span class="hljs-string">'.'</span>)
        sys.stdout.flush()
        <span class="hljs-keyword">if</span> len(val) &gt; <span class="hljs-number">0</span>:
            <span class="hljs-keyword">try</span>:
                response = urllib2.urlopen(req)
                args.output.write(response.read())
                time.sleep(<span class="hljs-number">.5</span>)
            <span class="hljs-keyword">except</span> urllib2.URLError <span class="hljs-keyword">as</span> e:
                <span class="hljs-keyword">print</span> (<span class="hljs-string">'%s'</span> % e)
    args.output.close()
    print(<span class="hljs-string">'Saved MP3 to %s'</span> % args.output.name)


<span class="hljs-function"><span class="hljs-keyword">def</span> <span class="hljs-title">text_to_speech_mp3_argparse</span><span class="hljs-params">()</span>:</span>
    description = <span class="hljs-string">'Google TTS Downloader.'</span>
    parser = argparse.ArgumentParser(description=description,
                                     epilog=<span class="hljs-string">'tunnel snakes rule'</span>)
    parser.add_argument(<span class="hljs-string">'-o'</span>, <span class="hljs-string">'--output'</span>,
                        action=<span class="hljs-string">'store'</span>, nargs=<span class="hljs-string">'?'</span>,
                        help=<span class="hljs-string">'Filename to output audio to'</span>,
                        type=argparse.FileType(<span class="hljs-string">'wb'</span>), default=<span class="hljs-string">'out.mp3'</span>)
    parser.add_argument(<span class="hljs-string">'-l'</span>, <span class="hljs-string">'--language'</span>,
                        action=<span class="hljs-string">'store'</span>,
                        nargs=<span class="hljs-string">'?'</span>,
                        help=<span class="hljs-string">'Language to output text to.'</span>, default=<span class="hljs-string">'en'</span>)
    group = parser.add_mutually_exclusive_group(required=<span class="hljs-keyword">True</span>)
    group.add_argument(<span class="hljs-string">'-f'</span>, <span class="hljs-string">'--file'</span>,
                       type=argparse.FileType(<span class="hljs-string">'r'</span>),
                       help=<span class="hljs-string">'File to read text from.'</span>)
    group.add_argument(<span class="hljs-string">'-s'</span>, <span class="hljs-string">'--string'</span>,
                       action=<span class="hljs-string">'store'</span>,
                       nargs=<span class="hljs-string">'+'</span>,
                       help=<span class="hljs-string">'A string of text to convert to speech.'</span>)
    <span class="hljs-keyword">if</span> len(sys.argv) == <span class="hljs-number">1</span>:
        parser.print_help()
        sys.exit(<span class="hljs-number">1</span>)
    <span class="hljs-keyword">return</span> parser.parse_args()


<span class="hljs-keyword">if</span> __name__ == <span class="hljs-string">"__main__"</span>:
    args = text_to_speech_mp3_argparse()
    <span class="hljs-keyword">if</span> args.file:
        input_text = args.file.read()
    <span class="hljs-keyword">if</span> args.string:
        input_text = <span class="hljs-string">' '</span>.join(map(str, args.string))
    audio_extract(input_text=input_text, args=args)
</code></pre>