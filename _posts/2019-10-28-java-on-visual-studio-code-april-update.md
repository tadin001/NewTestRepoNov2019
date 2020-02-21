---
ID: 222665
post_title: Java on Visual Studio Code April Update
author: sivyel
post_excerpt: ""
layout: post
permalink: >
  https://devblogs72.wpengine.com/visualstudio/java-on-visual-studio-code-april-update/
published: true
post_date: 2019-10-28 08:15:50
---
Welcome to April update! Java 12 is now officially supported with Visual Studio Code. We'd also like to show you some new and helpful code actions now available, along with new features from Debugger, Maven and CheckStyle. Try these new features by installing <a href="https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-pack" target="_blank" rel="noopener noreferrer">Java Extension Pack</a> with Visual Studio Code. See below for more details! 
### Java 12 Support Java is now updating with a faster pace and we're following closely. Thanks to the upstream update from JDT, you can build your project with Java 12 features now with VS Code as well. To use the experimental language features such as the new 

`switch` statement, add the following settings to `pom.xml`: <pre class="lang:default decode:true ">&lt;build&gt;
    &lt;plugins&gt;
        &lt;plugin&gt;
            &lt;groupId&gt;org.apache.maven.plugins&lt;/groupId&gt;
            &lt;artifactId&gt;maven-compiler-plugin&lt;/artifactId&gt;
            &lt;version&gt;3.8.0&lt;/version&gt;
            &lt;configuration&gt;
                &lt;source&gt;12&lt;/source&gt;
                &lt;compilerArgs&gt;--enable-preview&lt;/compilerArgs&gt;
            &lt;/configuration&gt;
        &lt;/plugin&gt;
    &lt;/plugins&gt;
&lt;/build&gt;</pre>

### Easier Getting Started Although Java has been there for a long time, it still attracts new developers, and we'd like to make sure it's easy enough for anyone to start programming Java with VS Code. One of the improvement we made recently is to provide you more detailed information to fix your environment setting. 

<img class="alignnone size-full wp-image-225017" src="https://devblogs.microsoft.com/visualstudio/wp-content/uploads/sites/4/2019/04/JDKDiagnostic.png" alt="" width="1024" height="768" /> What if you don't yet have JDK installed? No problem. When the Java extension pack is loaded, we will automatically detect whether a JDK is present. If not, we will provide you links to download reliable JDK at your choice. <img class="alignnone size-full wp-image-225017" src="https://devblogs.microsoft.com/visualstudio/wp-content/uploads/sites/4/2019/04/JDKInstall1.png" alt="" width="1024" height="768" /> Better yet, we're also working on a customized VS Code distribution which will help get you ready with everything needed for Java development with a single installer. To learn more, please <a name="#signup">sign up</a> at the end of this post to receive latest news and updates for Java on VS Code. 
### Performance Improvements We've been benchmarking and profiling the performance of VS Code for Java, on all platforms and major scenarios including loading and editing. There were several enhancement to improve performance in recent releases. 

*   Improved editing performance when dealing with large amount of source file opened in the editor
*   Optimize start up and load time with better server initilization and lazy downloading Java source As we try our best improving performance, it would still take some time when importing a big Java project to Visual Studio Code. In this case, it would be helpful to show more progress details and let you know what's actually happening behind the scene. Instead of just showing the percentage of progress, we now added detailed step information into the status, such as inspecting location, configuring project, updating Maven dependencies, refreshing workspace and build workspace to let you know the wait is meaningful. 

<img class="alignnone size-full wp-image-225074" src="https://devblogs.microsoft.com/visualstudio/wp-content/uploads/sites/4/2019/05/start-progress.jpg" alt="" width="1947" height="96" /> 
### More Code Actions Code actions are key to your productivity, so we keep bringing more of them to Visual Studio Code. 

##### Resolve ambiguous imports To deal with ambiguous imports, you now have a dropdown list to pick the right one. The code line with the unresolved type is also presented to you to help you decide. 

<img class="alignnone size-full wp-image-225039" src="https://devblogs.microsoft.com/visualstudio/wp-content/uploads/sites/4/2019/05/java.organize.imports.gif" alt="" width="1024" height="768" /> 
##### Generate hashCode() and equals() Now 

`hashCode()` & `equals()` can be generated with default implementations. All the non-static member variables are listed, and you can customize the generated code using the check list. There are two options for you to customize the generated code: 
*   If you use Java 7+, you can set `java.codeGeneration.hashCodeEquals.useJava7Objects` to `true` to generate shorter code which calls `Objects.hash` and `Objects.equals`.
*   You can also set `java.codeGeneration.hashCodeEquals.useInstanceof` to check the object type instead of calling `Object.getClass()`.

<img class="alignnone size-full wp-image-225041" src="https://devblogs.microsoft.com/visualstudio/wp-content/uploads/sites/4/2019/05/java.hashcode.equals.gif" alt="" width="1024" height="768" /> 
##### Generate toString() Picking which fields to be included in the 

`toString()` method and configure its template are all supported with the Generate `toString()` code action. <img class="alignnone size-full wp-image-225042" src="https://devblogs.microsoft.com/visualstudio/wp-content/uploads/sites/4/2019/05/java.generate.tostring.gif" alt="" width="1024" height="768" /> 
##### Extract to local variable To create a new variable (correctly typed) from the return value of an expression, the new quick fix 

`extract to local variable` provides a<span style="font-size: 1rem;"> quick fix bulb which appears when the cursor stops at the bracket </span>`()`<span style="font-size: 1rem;">. The keyboard shortcut is </span>`ctrl + .` <img class="alignnone size-full wp-image-225045" src="https://devblogs.microsoft.com/visualstudio/wp-content/uploads/sites/4/2019/05/extract_variable.gif" alt="" width="639" height="175" /> 
##### Override/Implement methods With this new source action, all the cadidates are presented to you with a checklist. Then you can decide what to override or implement. 

<img class="alignnone size-full wp-image-225040" src="https://devblogs.microsoft.com/visualstudio/wp-content/uploads/sites/4/2019/05/java.implement.methods.gif" alt="" width="1024" height="768" /> 
##### Add static import You can now convert static functions calls to static imports. 

<img class="alignnone size-full wp-image-225043" src="https://devblogs.microsoft.com/visualstudio/wp-content/uploads/sites/4/2019/05/java.convert.static.import.gif" alt="" width="1024" height="768" /> 
### Folding Range Now you can expand or collapse sections of code to make your Java file easy to read. We've enabled a couple popular ways for you to specify which code elements should be considered as a region to fold. 

<img class="alignnone size-full wp-image-225044" src="https://devblogs.microsoft.com/visualstudio/wp-content/uploads/sites/4/2019/05/java.folding.range_.gif" alt="" width="1024" height="768" /> 
### Debugger Updates Debugger is one of the most used extension in the Java extension family, and we're excited to show you the improvements below 

##### Display Logical Structure of Collections The debugger is now showing the logical structure of lists and maps, instead of the physical layout of the collections. If you prefer the physical layout view, you can go back by setting 

`java.debug.settings.showLogicalStructure` to `false`. <img class="alignnone size-full wp-image-225046" src="https://devblogs.microsoft.com/visualstudio/wp-content/uploads/sites/4/2019/05/java.debug_.logical.structure.gif" alt="" width="1024" height="768" /> 
##### Hightlight Exceptions in Editor Exceptions are now highlighted with extra info in the editor window. Before that, you need to hover on the exception to see details. Now the most important info is presented to you right at where it occurs. 

<img class="alignnone size-full wp-image-225047" src="https://devblogs.microsoft.com/visualstudio/wp-content/uploads/sites/4/2019/05/java.debug_.exception.view_.gif" alt="" width="1024" height="768" /> 
##### Go to Definition by Clicking Stack Trace in Debug Console When there an exception, you can now click on the stack trace to see the definition of the function calls. 

<img class="alignnone size-full wp-image-225048" src="https://devblogs.microsoft.com/visualstudio/wp-content/uploads/sites/4/2019/05/debug.gtd_.stack_.trace_.gif" alt="" width="1024" height="768" /> Other notable features include 
*   Auto-completion in debug console for types without source code
*   Auto shorten the command line when file name or extension is too long.

<a name="maven-update"></a> 
### Maven Updates And a couple new features for Maven as well. 

##### Debug Maven Plug-in Goal Now you can easily configure your breakpoint and start debug any Maven goals with just a couple clicks. 

### <img class="alignnone size-full wp-image-225050" src="https://devblogs.microsoft.com/visualstudio/wp-content/uploads/sites/4/2019/05/debug-maven-plugin-goal.gif" alt="" width="1024" height="768" />

##### Customize maven commands Now you are able to specify your favorite commands in settings for future execution. 

<img class="alignnone size-full wp-image-225051" src="https://devblogs.microsoft.com/visualstudio/wp-content/uploads/sites/4/2019/05/favorite-commands.gif" alt="" width="1024" height="768" /> 
##### Show Dependency Tree We also support showing dependencies in a tree view which allows you to inspect all dependencies in your project at a single place and check for potential issues. 

<img class="alignnone size-full wp-image-225049" src="https://devblogs.microsoft.com/visualstudio/wp-content/uploads/sites/4/2019/05/show-dependency-tree.gif" alt="" width="1024" height="768" /> One more thing. There's one more s<span style="font-size: 1rem;">hortcut to add dependencies. </span><span style="font-size: 1rem;">When editing a POM file, there is a shortcut command to search and add a dependency. Try </span>`Command Palette -> Maven: Add a dependency`<span style="font-size: 1rem;">.</span> 
### Sign up {#signup} If you'd like to follow the latest of Java on VS Code, please provide your email with us using the form below. We will send out updates and tips every couple weeks and invite you to test our unreleased feature and provide feedback early on. 

<div data-form-block-id="a98bf458-e066-e911-a96e-000d3a340154">
</div>

<script src="https://mktdplp102cdn.azureedge.net/public/1.35.1026.0/static/js/form-loader.js"></script> <div id="dgCPdzqBMykwIL6XsCcP3tC9zZGvAAN-t3ma0GiZE0QU">
</div>

<script language="javascript" type="text/javascript">(function (id, f, t, ws, ms_tr_il_08, ms_tr_il_w_01) { var tr = function (cb) { var count = 0; var callback = function () { if (count == 0) { count++; if (w) { w.w(id, t, cb); } } }; var ts = document.createElement('script'); ts.src = ws; ts.type = 'text/javascript'; ts.onload = callback; ts.onreadystatechange = function () { if (this.readyState == 'complete' || this.readyState == 'loaded') { callback(); } }; var head = document.getElementsByTagName('head')[0]; head.appendChild(ts); }; if (typeof ms_tr_il_08 === 'function') { if (ms_tr_il_w_01 === null) { tr(function() { ms_tr_il_08(id, f, t); }); } else { ms_tr_il_w_01.w(id, t, function(websiteVisitedParams) { ms_tr_il_08(id, f, t, websiteVisitedParams); }); } } else { tr(); }})('gCPdzqBMykwIL6XsCcP3tC9zZGvAAN-t3ma0GiZE0QU', 'https://5a3318f6fcc34e41bf99d46845944055.svc.dynamics.com/f', 'https://5a3318f6fcc34e41bf99d46845944055.svc.dynamics.com/t', 'https://5a3318f6fcc34e41bf99d46845944055.svc.dynamics.com/t/w', typeof ms_tr_il_08 === "undefined" ? null : ms_tr_il_08, typeof ms_tr_il_w_01 === "undefined" ? null : ms_tr_il_w_01);</script> 
### Try it out Please don’t hesitate to give it a try! Your feedback and suggestions are very important to us and will help shape our product in future. You may take this 

<a href="https://www.research.net/r/vscodejava-blog?o=%5bo_value%5d&m=%5bm_value%5d" target="_blank" rel="noopener noreferrer">survey</a> to share your thoughts! Visual Studio Code is a fast and lightweight code editor with great Java support from many extensions 
*   <a href="https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-pack" target="_blank" rel="noopener noreferrer">Java Extension Pack</a> includes essential Java tools including <a href="https://marketplace.visualstudio.com/items?itemName=redhat.java" target="_blank" rel="noopener noreferrer">Language Support for Java™ by Red Hat</a>, <a href="https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-debug" target="_blank" rel="noopener noreferrer">Debugger for Java</a>, <a href="https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-maven" target="_blank" rel="noopener noreferrer">Maven</a>, <a href="https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-test" target="_blank" rel="noopener noreferrer">Java Test Runner</a> and <a href="https://go.microsoft.com/fwlink/?linkid=2006060" target="_blank" rel="noopener noreferrer">IntelliCode Extension for Visual Studio Code</a>.
*   There're also other Java related extensions you can choose from, including 
    *   <a href="https://marketplace.visualstudio.com/items?itemName=adashen.vscode-tomcat" target="_blank" rel="noopener noreferrer">Tomcat</a> and <a href="https://marketplace.visualstudio.com/items?itemName=SummerSun.vscode-jetty" target="_blank" rel="noopener noreferrer">Jetty</a> for quickly deploy and manage local app servers.
    *   In case you’re working on Spring Boot, there’re also great support provided by <a href="https://marketplace.visualstudio.com/items?itemName=Pivotal.vscode-boot-dev-pack" target="_blank" rel="noopener noreferrer">Pivotal</a> and <a href="https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-spring-initializr" target="_blank" rel="noopener noreferrer">Microsoft</a> available on Visual Studio Code including <a href="https://marketplace.visualstudio.com/items?itemName=Pivotal.vscode-spring-boot" target="_blank" rel="noopener noreferrer">Spring Boot Tools</a>, <a href="https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-spring-initializr" target="_blank" rel="noopener noreferrer">Spring Initializr</a> and <a href="https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-spring-boot-dashboard" target="_blank" rel="noopener noreferrer">Spring Boot Dashboard</a>.
    *   <a href="https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-dependency" target="_blank" rel="noopener noreferrer">Java Dependencies</a> provides you a package view of your Java project and helps you managing your dependencies.
    *   <a href="https://marketplace.visualstudio.com/items?itemName=shengchen.vscode-checkstyle" target="_blank" rel="noopener noreferrer">Checkstyle</a> could be handy when you need coherence code style especially cross multiple team members.
*   Learn more about <a href="https://code.visualstudio.com/docs/languages/java" target="_blank" rel="noopener noreferrer">Java on Visual Studio Code</a>.
*   Explore our step by step <a href="https://code.visualstudio.com/docs/java/java-tutorial" target="_blank" rel="noopener noreferrer">Java Tutorials on Visual Studio Code</a>.