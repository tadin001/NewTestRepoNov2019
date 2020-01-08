---
ID: 222728
post_title: Hello World in various code languages
author: qadevblogs
post_excerpt: ""
layout: post
permalink: >
  https://devblogs72.wpengine.com/visualstudio/hello-world-in-various-code-languages/
published: true
post_date: 2020-01-07 22:05:25
---
Visual Editor

Ref blog blog : https://excelwithbusiness.com/blog/say-hello-world-in-28-different-programming-languages/

 

## [ALGOL][1]

A contemporary of the other early 1950’s programming languages FORTRAN, Lisp, and COBOL. It became the standard way of describing algorithms in academia for 30 years, meaning it influenced many other languages’ syntaxes, including C.

<pre>BEGIN DISPLAY("HELLO WORLD!") END.</pre>

## [ASPECTJ][2]

The de facto standard for the style of programming called Aspect Oriented Programming (AOP). AOP is not popular but loved by some and its concepts do find their way into other languages and libraries. AspectJ uses a Java-like syntax.

<pre class="prettyprint prettyprinted"><span class="com">// HelloWorld.java</span>
<span class="kwd">public</span> <span class="kwd">class</span> <span class="typ">HelloWorld</span> <span class="pun">{</span>
    <span class="kwd">public</span> <span class="kwd">static</span> <span class="kwd">void</span><span class="pln"> say</span><span class="pun">(</span><span class="typ">String</span><span class="pln"> message</span><span class="pun">)</span> <span class="pun">{</span>
        <span class="typ">System</span><span class="pun">.</span><span class="kwd">out</span><span class="pun">.</span><span class="pln">println</span><span class="pun">(</span><span class="pln">message</span><span class="pun">);</span>
    <span class="pun">}</span>

    <span class="kwd">public</span> <span class="kwd">static</span> <span class="kwd">void</span><span class="pln"> sayToPerson</span><span class="pun">(</span><span class="typ">String</span><span class="pln"> message</span><span class="pun">,</span> <span class="typ">String</span><span class="pln"> name</span><span class="pun">)</span> <span class="pun">{</span>
        <span class="typ">System</span><span class="pun">.</span><span class="kwd">out</span><span class="pun">.</span><span class="pln">println</span><span class="pun">(</span><span class="pln">name </span><span class="pun">+</span> <span class="str">", "</span> <span class="pun">+</span><span class="pln"> message</span><span class="pun">);</span>
    <span class="pun">}</span>
<span class="pun">}

</span></pre>

<pre class="prettyprint prettyprinted"><span class="com">// MannersAspect.java</span>
<span class="kwd">public</span><span class="pln"> aspect </span><span class="typ">MannersAspect</span> <span class="pun">{</span><span class="pln">
    pointcut callSayMessage</span><span class="pun">()</span> <span class="pun">:</span><span class="pln"> call</span><span class="pun">(</span><span class="kwd">public</span> <span class="kwd">static</span> <span class="kwd">void</span> <span class="typ">HelloWorld</span><span class="pun">.</span><span class="pln">say</span><span class="pun">*(..));</span><span class="pln">
    before</span><span class="pun">()</span> <span class="pun">:</span><span class="pln"> callSayMessage</span><span class="pun">()</span> <span class="pun">{</span>
        <span class="typ">System</span><span class="pun">.</span><span class="kwd">out</span><span class="pun">.</span><span class="pln">println</span><span class="pun">(</span><span class="str">"Good day!"</span><span class="pun">);</span>
    <span class="pun">}</span><span class="pln">
    after</span><span class="pun">()</span> <span class="pun">:</span><span class="pln"> callSayMessage</span><span class="pun">()</span> <span class="pun">{</span>
        <span class="typ">System</span><span class="pun">.</span><span class="kwd">out</span><span class="pun">.</span><span class="pln">println</span><span class="pun">(</span><span class="str">"Thank you!"</span><span class="pun">);</span>
    <span class="pun">}</span>
<span class="pun">}</span></pre>

## [APPLESCRIPT][3]

If you’re on a Mac you can use this to automate and customise your applications.

<pre class=" hljs vbnet"><span class="nb">say</span> <span class="s2"><span class="hljs-string">"Hello, world!"</span></span></pre>

## [ASSEMBLY LANGUAGE][4]

This is the language that will get you the highest performing and most efficient software that is still human-readable. It’s so hard to write in that it only makes sense to use it for small parts of a programme that are performance-sensitive. You will find it in operating systems and 3D game engines.

<pre class="default prettyprint prettyprinted"><code>    &lt;span class="kwd">global&lt;/span>&lt;span class="pln">  _main
    &lt;/span>&lt;span class="kwd">extern&lt;/span>&lt;span class="pln">  _printf

    section &lt;/span>&lt;span class="pun">.&lt;/span>&lt;span class="pln">text
_main&lt;/span>&lt;span class="pun">:&lt;/span>&lt;span class="pln">
    push    message
    call    _printf
    add     esp&lt;/span>&lt;span class="pun">,&lt;/span> &lt;span class="lit">4&lt;/span>&lt;span class="pln">
    ret
message&lt;/span>&lt;span class="pun">:&lt;/span>&lt;span class="pln">
    db  &lt;/span>&lt;span class="str">'Hello, World'&lt;/span>&lt;span class="pun">,&lt;/span> &lt;span class="lit">10&lt;/span>&lt;span class="pun">,&lt;/span> &lt;span class="lit">0&lt;/span></code></pre>

## [BASH (UNIX SHELL)][5]

Used to interact with and manage Linux and Unix system at the command line.

<pre>#!/bin/bash
STR="Hello World!"
echo $STR</pre>

## BASIC

Basic was first released in 1964 and reached its heyday in the early 80s, when computers were starting to enter the small office and the home. You were expected to write your own software and the large majority of computers shipped with some version of BASIC. It hit the sweet spot of being easy to learn but lean enough to run on this underpowered hardware.

There are a huge number of BASIC variants, Visual Basic was a variation that was very popular on Windows in the 90s. This was replaced by Visual Basic .NET (now called just Visual Basic) but was quite different from the earlier versions. Visual Basic is still widely used.

<pre><span class="nl">10</span> <span class="kr">PRINT</span> <span class="s2">"Hello, World!"</span>
<span class="nl">20</span> <span class="kr">END</span></pre>

## [C][6]

The most important language in the world. It’s what operating systems like Windows, MacOS, iOS, and Android are written in, as well as browsers and 3D games engines. Its syntax has influenced countless other programming languages.

C maps closely to Assembly Language but you can write more complex programmes with it. If you need the highest performance possible without losing your mind then C is for you.

C is also the language that made “Hello, World” examples popular.

<pre><span class="cp">#include</span> <span class="cpf">&lt;stdio.h&gt;</span>
<span class="kt">int</span> <span class="nf">main</span><span class="p">(</span><span class="kt">void</span><span class="p">)</span>
<span class="p">{</span>
    <span class="n">printf</span><span class="p">(</span><span class="s">"hello, world</span><span class="se">\n</span><span class="s">"</span><span class="p">);</span>
<span class="p">}</span></pre>

## [C++][7]

Has performance close to C and is used in many important projects like the Chrome Browser. C++ was an effort to make a language that was easier to build large projects with while still being fast and efficient.

<pre><span class="cp">#include</span> <span class="cpf">&lt;iostream&gt;</span>
<span class="kt">int</span> <span class="nf">main</span><span class="p">()</span>
<span class="p">{</span>
    <span class="n">std</span><span class="o">::</span><span class="n">cout</span> <span class="o">&lt;&lt;</span> <span class="s">"Hello, world!</span><span class="se">\n</span><span class="s">"</span><span class="p">;</span>
    <span class="k">return</span> <span class="mi">0</span><span class="p">;</span>
<span class="p">}</span></pre>

## [C#][8]

Created when Microsoft built their .Net virtual machine. C# has become Microsoft premier programming language.

<pre><span class="k">using</span> <span class="nn">System</span><span class="p">;</span>
<span class="k">class</span> <span class="nc">Program</span>
<span class="p">{</span>
    <span class="k">static</span> <span class="k">void</span> <span class="nf">Main</span><span class="p">(</span><span class="kt">string</span><span class="p">[]</span> <span class="n">args</span><span class="p">)</span>
    <span class="p">{</span>
        <span class="n">Console</span><span class="p">.</span><span class="n">WriteLine</span><span class="p">(</span><span class="s">"Hello, world!"</span><span class="p">);</span>
    <span class="p">}</span>
<span class="p">}</span></pre>

## [CAML (OCAML)][9]

A functional programming focused language in the ML family of languages. It’s used for a number of smaller projects at Facebook. The compiler for Facebook’s Hack language was written in OCaml.

<pre><span class="n">print_endline</span> <span class="s2">"Hello, world!"</span><span class="o">;;</span></pre>

## [CLOJURE (CLOJURESCRIPT)][10]

A functional programming language intended to be a modern take on Lisp. It runs on the Java virtual machine or complies down to JavaScript.

<pre><span class="p">(</span><span class="nb">println </span><span class="s">"Hello world!"</span><span class="p">)</span></pre>

## [COBOL][11]

Once very popular in the era of mainframe computing. It’s now in decline and many COBOL programs are being ported to other languages.

<pre><span class="kr">IDENTIFICATION</span> <span class="kr">DIVISION</span><span class="p">.</span>
       <span class="kr">PROGRAM-ID</span><span class="p">.</span> <span class="nv">hello-world</span><span class="p">.</span>
       <span class="kr">PROCEDURE</span> <span class="kr">DIVISION</span><span class="p">.</span>
           <span class="kr">DISPLAY </span><span class="s2">"Hello, world!"</span>
           <span class="p">.</span></pre>

## [COFFEESCRIPT][12]

An effort to make JavaScript better to work with.

<pre><span class="nx">console</span><span class="p">.</span><span class="nx">log</span> <span class="s">"Hello, World!"</span></pre>

## [DART][13]

A language for building client-side software that can run on phones and browsers. Google is using Dart in some of its most important projects.

<pre><span class="n">main</span><span class="p">()</span> <span class="p">{</span>
  <span class="n">print</span><span class="p">(</span><span class="s1">'Hello World!'</span><span class="p">);</span>
<span class="p">}</span></pre>

## [DBASE][14] ([FOXPRO][15])

dBase is a collection of tools: a programming language, a database, forms. In its time it was very popular but now has fallen out of use. A popular clone was FoxPro.

<pre>? "Hello World"</pre>

## [DELPHI][16] ([OBJECT PASCAL][17])

Delphi was really a rapid application development (RAD) tool that used the Object Pascal language. In the mid- to late 90s, it was beloved by many programmers for writing Windows programmes. It’s no longer used, but still loved.

<pre><span class="k">procedure</span> <span class="nc">TForm1</span><span class="o">.</span><span class="nf">ShowAMessage</span><span class="o">;</span>
<span class="k">begin</span>
  <span class="n">ShowMessage</span><span class="p">(</span><span class="s">'Hello World!'</span><span class="p">)</span><span class="o">;</span>
<span class="k">end</span><span class="o">;</span></pre>

## [EIFFEL][18]

The language goes hand-in-hand with a way of writing software called the Eiffel Method. Eiffel introduced the concept of “design by contract” which is now used in many other languages.

<pre><span class="kr">class</span>
    <span class="nc">HELLO_WORLD</span>
<span class="kr">create</span>
    <span class="n">make</span>
<span class="kr">feature</span>
    <span class="n">make</span>
        <span class="kr">do</span>
            <span class="n">print</span> <span class="p">(</span><span class="s">"Hello, world!%N"</span><span class="p">)</span>
        <span class="kr">end</span>
<span class="kr">end</span></pre>

## [ERLANG][19]

Designed to work in a distributed way to provide real-time processing and high availability. Popular for phone systems but not well-know until it was used for CouchDB, the project that was the catalyst for the NoSQL movement.

<pre>-module(hello).
 -export([hello_world/0]).

 hello_world() -&gt; io:fwrite("hello, world\n").</pre>

## [ELIXIR][20]

While Erlang is great at a technical level, programmers find it hard to work with. Elixir uses Erlang’s technology while providing an easier experience for programmers.

<pre><span class="nc">IO</span><span class="o">.</span><span class="n">puts</span> <span class="s2">"Hello World!"</span></pre>

## [F#][21]

A functional focused programming language that runs on the .NET framework.

<pre><span class="k">open</span> <span class="nn">System</span>
<span class="nn">Console</span><span class="p">.</span><span class="n">WriteLine</span><span class="o">(</span><span class="s">"Hello World!"</span><span class="o">)</span></pre>

## [FORTRAN][22]

Created in the 1950s to run on mainframe computers, it’s well suited for numerical and scientific work. It became standard in the scientific world where it’s still used today.

<pre><span class="k">program </span><span class="n">helloworld</span>
     <span class="k">print</span> <span class="o">*</span><span class="p">,</span> <span class="s2">"Hello world!"</span>
<span class="k">end program </span><span class="n">helloworld</span></pre>

## [GO][23]

Go was created and used at Google. It’s a practical language that focuses on programmer productivity with a community focused on performance and low latency.

<pre><span class="kn">package</span> <span class="nx">main</span>
<span class="kn">import</span> <span class="s">"fmt"</span>
<span class="kd">func</span> <span class="nx">main</span><span class="p">()</span> <span class="p">{</span>
    <span class="nx">fmt</span><span class="p">.</span><span class="nx">Println</span><span class="p">(</span><span class="s">"Hello, World"</span><span class="p">)</span>
<span class="p">}</span></pre>

## [GROOVY (RUBY)][24]

A dynamically typed scripting language that runs in the Java runtime. Most Java code would also run as Groovy code but Groovy code can be more compact as it doesn’t require everything that Java does.

<pre>println "Hello World"</pre>

## [HASKELL][25]

A strongly-typed, purely functional programming language.

<pre><span class="kr">module</span> <span class="nn">Main</span> <span class="kr">where</span>
<span class="nf">main</span> <span class="ow">::</span> <span class="kt">IO</span> <span class="nb">()</span>
<span class="nf">main</span> <span class="ow">=</span> <span class="n">putStrLn</span> <span class="s">"Hello, World!"</span></pre>

## [IBM RPG][26]

First seen in 1959, created by IBM to run on its hardware. It’s one of the few languages originally designed for punch cards that are still in use today.

<pre>dcl-s wait char(1);

dsply ( 'Hello World!') ' ' wait;

*inlr = *on;</pre>

## [JAVA][27]

Something that made Java special is that it was designed so you could write code once and then allow it to run on any operation system. Java is the most popular programming language in the world. It’s used to teach students and in large companies. All Android apps are written in Java.

<pre><span class="kd">class</span> <span class="nc">HelloWorldApp</span> <span class="o">{</span>
    <span class="kd">public</span> <span class="kd">static</span> <span class="kt">void</span> <span class="nf">main</span><span class="o">(</span><span class="n">String</span><span class="o">[]</span> <span class="n">args</span><span class="o">)</span> <span class="o">{</span>
        <span class="n">System</span><span class="o">.</span><span class="na">out</span><span class="o">.</span><span class="na">println</span><span class="o">(</span><span class="s">"Hello World!"</span><span class="o">);</span> <span class="c1">// Prints the string to the console.</span>
    <span class="o">}</span>
<span class="o">}</span></pre>

## [JAVASCRIPT (ECMASCRIPT)][28]

JavaScript is the most commonly found programming language in the world. Mainly because it is required to be in every web browser. JavaScript is what makes the web dynamic and interactive. It was standardised under the name ECMAScript.

<pre><span class="nx">console</span><span class="p">.</span><span class="nx">log</span><span class="p">(</span><span class="s2">"Hello World!"</span><span class="p">);</span></pre>

## JULIA

<span class="kw1">println</span><span class="br0">(</span><span class="st0">"Hello, World!"</span><span class="br0">)</span>

julia hello-world.jl

## [LISP][29]

Designed a year after Fortran, Lisp is the second-oldest high-level programming language that’s still in common use. Lisp can lay claim to many programming language firsts, and can now be considered a family of languages as well as a language itself. It was popular in the 70s era of AI research. It seemed to be fading in popularity in the 90s but is now gaining popularity through several new dialects.

<pre><span class="nb">(print</span> <span class="s">"Hello world"</span><span class="p">)</span></pre>

## [LOGO][30]

Intended for education use, Logo has a close association with teaching graphical concepts. Popular in the 80s, a student would direct an on-screen “turtle” to draw lines. Some lucky students would also have a real robotic turtle to draw the same lines on actual paper.

<pre>TO HELLO
        PRINT [Hello world]
        END</pre>

## [LUA][31]

What makes Lua great is how easy it is to embed into software.

<pre><span class="nb">print</span><span class="p">(</span><span class="s2">"Hello World!"</span><span class="p">)</span></pre>

## [MACHINE CODE][32]

Machine code is the lowest level of instruction you can send to a CPU. Machine code is not really readable by humans and humans can only do trivial things in it but all software is eventually turned into Machine code before it’s sent to the CPU.

    b8    21 0a 00 00   #moving "!\n" into eax
    a3    0c 10 00 06   #moving eax into first memory location
    b8    6f 72 6c 64   #moving "orld" into eax
    a3    08 10 00 06   #moving eax into next memory location
    b8    6f 2c 20 57   #moving "o, W" into eax
    a3    04 10 00 06   #moving eax into next memory location
    b8    48 65 6c 6c   #moving "Hell" into eax
    a3    00 10 00 06   #moving eax into next memory location
    b9    00 10 00 06   #moving pointer to start of memory location into ecx
    ba    10 00 00 00   #moving string size into edx
    bb    01 00 00 00   #moving "stdout" number to ebx
    b8    04 00 00 00   #moving "print out" syscall number to eax
    cd    80            #calling the linux kernel to execute our print to stdout
    b8    01 00 00 00   #moving "sys_exit" call number to eax
    cd    80            #executing it via linux sys_call

## [MATHEMATICA (WOLFRAM LANGUAGE)][33]

A programme with a dedicated programming language, popular in science and maths for doing complex calculations.

<pre>CloudDeploy["Hello, World"]</pre>

## [MATLAB][34]

A combination of a programme and a language. Used to analyse data and develop algorithms. It’s used in education to teach linear algebra and numerical analysis. It’s also popular with scientists doing work with image manipulation.

<pre><span class="k">classdef</span> <span class="n">hello</span>
    <span class="k">methods</span>
<span class="k">        function</span> <span class="nf">greet</span><span class="p">(</span>this<span class="p">)</span>
            <span class="nb">disp</span><span class="p">(</span><span class="s">'Hello, World'</span><span class="p">)</span>
        <span class="k">end</span>
    <span class="k">end</span>
<span class="k">end</span></pre>

## [ML][35]

A functional language that is derived from Lisp but with a strong type system.

<pre><span class="n">print</span> <span class="s2">"Hello world!</span><span class="se">\n</span><span class="s2">"</span><span class="p">;</span></pre>

## [NODE.JS][36]

Not so much a language (the language used is JavaScript) but a runtime environment to run JavaScript on servers as opposed to browsers. The goal was to demonstrate that asynchronous programming was better for modern multi-core CPUs. It now gets used a great deal for tooling of large front-end projects.

<pre><span class="nx">console</span><span class="p">.</span><span class="nx">log</span><span class="p">(</span><span class="s2">"Hello World!"</span><span class="p">);</span></pre>

## [OBJECTIVE-C][37]

An extension of C that adds Smalltalk like messaging. Used by Apple in writing macOS and iOS.

<pre>main()
{
  puts("Hello World!");
  return 0;
}</pre>

## [PASCAL][38]

A popular language in the 80s and 90s especially for teaching programming. It evolved a great deal and was also the language used in the Delphi RAD toolset.

<pre><span class="k">program</span> <span class="n">HelloWorld</span><span class="p">(</span><span class="n">output</span><span class="p">)</span><span class="o">;</span>
<span class="k">begin</span>
  <span class="nb">Write</span><span class="p">(</span><span class="s">'Hello, world!'</span><span class="p">)</span>
<span class="k">end</span><span class="o">.</span></pre>

## [PERL][39]

Perl is very powerful for text processing. A popular option for creating websites in the early days of dynamic websites.

<pre><span class="k">print</span> <span class="s">"Hello, World!\n"</span><span class="p">;</span></pre>

## [PHP][40]

PHP is the most popular language for building the backend of websites. It’s what Facebook and WordPress are written in. Facebook decided to create their own dialect of PHP called [Hack][41].

<pre>&lt;?php echo "Hello, World";</pre>

## [POWERSHELL][42]

Used to interact with and manage Windows systems at the command line level.

<pre>Write-Host "Hello, World!"</pre>

## [PYTHON][43]

Has a compact syntax needing far fewer lines of code than languages like Java or C++. It’s very popular and is used for websites and artificial intelligence (AI) tasks.

<pre>print("Hello World")


<span style="font-size: 24pt;">QSharp</span> 

<span class="hljs-function"><span class="hljs-keyword">operation</span> TestBellState(<span class="hljs-params">count : <span class="hljs-keyword">Int</span>, initial : <span class="hljs-keyword">Result</span></span>) : (<span class="hljs-params"><span class="hljs-keyword">Int</span>, <span class="hljs-keyword">Int</span></span>) </span>{

    <span class="hljs-keyword">mutable</span> numOnes = <span class="hljs-number">0</span>;
    <span class="hljs-keyword">using</span> (qubit = <span class="hljs-keyword">Qubit</span>()) {

        <span class="hljs-control">for</span> (test <span class="hljs-control">in</span> <span class="hljs-number">1.</span>.count) {
            Set(initial, qubit);
            <span class="hljs-keyword">let</span> res = <span class="hljs-helper">M</span>(qubit);

            <span class="hljs-comment">// Count the number of ones we saw:</span>
            <span class="hljs-control">if</span> (res == <span class="hljs-constant">One</span>) {
                <span class="hljs-keyword">set</span> numOnes += <span class="hljs-number">1</span>;
            }
        }
        Set(<span class="hljs-constant">Zero</span>, qubit);
    }

    <span class="hljs-comment">// Return number of times we saw a |0&gt; and number of times we saw a |1&gt;</span>
    <span class="hljs-control">return</span> (count-numOnes, numOnes);
}</pre>

## [R][44]

A great language for doing statistics, and a popular choice in the scientific world.

<pre>cat("Hello world\n")</pre>

## [RPG][26]

An old programing language that has been able to stay around by continually evolving. With origins in the punch card era, it is now found mostly on IBM hardware.

<pre>dcl-s wait char(1);

dsply ( 'Hello World!') ' ' wait;

*inlr = *on;</pre>

## [RUBY][45]

Designed to be a productive and fun language to use, stressing human needs over computer needs. The Rails web framework was written for Ruby, and had a huge impact on web framework design. Ruby is still a popular language for creating websites.

<pre><span class="nb">puts</span> <span class="s1">'Hello World!'</span></pre>

## [RUST][46]

A new language that is intended to replace languages like C for doing systems-level work. Parts of Firefox are being replaced with Rust.

<pre><span class="k">fn</span> <span class="nf">main</span><span class="p">()</span> <span class="p">{</span>
    <span class="n">println</span><span class="o">!</span><span class="p">(</span><span class="s">"Hello, world!"</span><span class="p">);</span>
<span class="p">}</span></pre>

## [SCALA][47]

Designed to address some of the criticisms of Java. A function-focused language that runs on the Java virtual machine.

<pre><span class="k">object</span> <span class="nc">HelloWorld</span> <span class="k">extends</span> <span class="nc">App</span> <span class="o">{</span>
   <span class="n">println</span><span class="o">(</span><span class="s">"Hello, World!"</span><span class="o">)</span>
 <span class="o">}</span></pre>

## [SCHEME][48]

One of the two main dialects of Lisp, the other being Common List. It tried to be minimalistic in design and allow powerful extension of the language.

<pre><span class="p">(</span><span class="k">let </span><span class="p">((</span><span class="nf">hello0</span> <span class="p">(</span><span class="nf">lambda</span><span class="p">()</span> <span class="p">(</span><span class="nb">display </span><span class="s">"Hello world"</span><span class="p">)</span> <span class="p">(</span><span class="nf">newline</span><span class="p">))))</span>
  <span class="p">(</span><span class="nf">hello0</span><span class="p">))</span></pre>

## [SCRATCH][49]

A visual programming language designed to let kids learn skills by programming. There is also Scratch Jr. which is intended for use by 5-7 year olds. Both languages are used by millions in and out of schools all over the world.

    <span class="n">say</span> <span class="n">Hello</span><span class="p">,</span> <span class="n">World</span><span class="o">!</span>

## [SELF][50]

A dialect of Smalltalk, it was the first language to use prototype-based programming, something that JavaScript uses.

<pre><span class="s">'Hello, World!'</span> <span class="nf">print</span><span class="p">.</span></pre>

## [SMALLTALK][51]

A very important language that has had a massive influence on many programming languages. It was also popular with people who would popularise programming best practices. Many things that are now common in programming were first done in Smalltalk.

<pre>Transcript show: 'Hello World!'.</pre>

## [SWIFT][52]

A newer language created at Apple that is being promoted to replace Objective-C for use on its platforms. It’s designed to be an easier language to learn and use without losing the performance of Objective-C.

<pre>println("Hello, world!")</pre>

## [TCL][53]

Used in combination with the Tk extension, Tcl/Tk is popular for creating graphical user interfaces.

<pre>puts "Hello World!"</pre>

## [TYPESCRIPT][54]

Designed in Microsoft, it’s a dialect of JavaScript that adds strict rules to help with large projects while remaining compatible with JavaScript.

<pre><span class="nx">console</span><span class="p">.</span><span class="nx">log</span><span class="p">(</span><span class="s2">"Hello World!"</span><span class="p">);</span></pre>

 [1]: https://en.wikipedia.org/wiki/ALGOL
 [2]: https://en.wikipedia.org/wiki/AspectJ
 [3]: https://en.wikipedia.org/wiki/AppleScript
 [4]: https://en.wikipedia.org/wiki/Assembly_language
 [5]: https://en.wikipedia.org/wiki/Bash_(Unix_shell)
 [6]: https://en.wikipedia.org/wiki/C_(programming_language)
 [7]: https://en.wikipedia.org/wiki/C%2B%2B
 [8]: https://en.wikipedia.org/wiki/C_Sharp_(programming_language)
 [9]: https://en.wikipedia.org/wiki/Caml
 [10]: https://en.wikipedia.org/wiki/Clojure
 [11]: https://en.wikipedia.org/wiki/COBOL
 [12]: https://en.wikipedia.org/wiki/CoffeeScript
 [13]: https://en.wikipedia.org/wiki/Dart_(programming_language)
 [14]: https://en.wikipedia.org/wiki/DBase
 [15]: https://en.wikipedia.org/wiki/FoxPro
 [16]: https://en.wikipedia.org/wiki/Delphi_(programming_language)
 [17]: https://en.wikipedia.org/wiki/Object_Pascal
 [18]: https://en.wikipedia.org/wiki/Eiffel_(programming_language)
 [19]: https://en.wikipedia.org/wiki/Erlang_(programming_language)
 [20]: https://en.wikipedia.org/wiki/Elixir_(programming_language)
 [21]: https://en.wikipedia.org/wiki/F_Sharp_(programming_language)
 [22]: https://en.wikipedia.org/wiki/Fortran
 [23]: https://en.wikipedia.org/wiki/Go_(programming_language)
 [24]: https://en.wikipedia.org/wiki/Groovy_(programming_language)
 [25]: https://en.wikipedia.org/wiki/Haskell_(programming_language)
 [26]: https://en.wikipedia.org/wiki/IBM_RPG
 [27]: https://en.wikipedia.org/wiki/Java_(programming_language)
 [28]: https://en.wikipedia.org/wiki/JavaScript
 [29]: https://en.wikipedia.org/wiki/Lisp_(programming_language)
 [30]: https://en.wikipedia.org/wiki/Logo_(programming_language)
 [31]: https://en.wikipedia.org/wiki/Lua_(programming_language)
 [32]: https://en.wikipedia.org/wiki/Machine_code
 [33]: https://en.wikipedia.org/wiki/Wolfram_Mathematica
 [34]: https://en.wikipedia.org/wiki/MATLAB
 [35]: https://en.wikipedia.org/wiki/ML_(programming_language)
 [36]: https://en.wikipedia.org/wiki/Node.js
 [37]: https://en.wikipedia.org/wiki/Objective-C
 [38]: https://en.wikipedia.org/wiki/Pascal_(programming_language)
 [39]: https://en.wikipedia.org/wiki/Perl
 [40]: https://en.wikipedia.org/wiki/PHP
 [41]: https://en.wikipedia.org/wiki/Hack_(programming_language)
 [42]: https://en.wikipedia.org/wiki/PowerShell
 [43]: https://en.wikipedia.org/wiki/Python_(programming_language)
 [44]: https://en.wikipedia.org/wiki/R_(programming_language)
 [45]: https://en.wikipedia.org/wiki/Ruby_(programming_language)
 [46]: https://en.wikipedia.org/wiki/Rust_(programming_language)
 [47]: https://en.wikipedia.org/wiki/Scala_(programming_language)
 [48]: https://en.wikipedia.org/wiki/Scheme_(programming_language)
 [49]: https://en.wikipedia.org/wiki/Scratch_(programming_language)
 [50]: https://en.wikipedia.org/wiki/Self_(programming_language)
 [51]: https://en.wikipedia.org/wiki/Smalltalk
 [52]: https://en.wikipedia.org/wiki/Swift_(programming_language)
 [53]: https://en.wikipedia.org/wiki/Tcl
 [54]: https://en.wikipedia.org/wiki/TypeScript