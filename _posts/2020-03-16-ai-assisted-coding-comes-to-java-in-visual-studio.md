---
ID: 222765
post_title: >
  AI-assisted Coding Comes to Java in
  Visual Studio
author: Sivakumar Kodidala
post_excerpt: ""
layout: post
permalink: >
  https://devblogs72.wpengine.com/visualstudio/ai-assisted-coding-comes-to-java-in-visual-studio/
published: true
post_date: 2020-03-16 03:35:47
---
<a target="_blank" href="https://visualstudio.microsoft.com/services/intellicode/" rel="noopener noreferrer">Visual Studio IntelliCode</a> is a set of AI-assisted capabilities that aims to improve developer productivity with features like AI-assisted IntelliSense and statement completion, code formatting, and style rule inference. During <a target="_blank" href="https://springoneplatform.io/" rel="noopener noreferrer">SpringOne 2018</a>, we announced that we will bring those productivity boosters to Java developers and now we’re happy to introduce AI-assisted IntelliSense to Java in the <a target="_blank" href="https://go.microsoft.com/fwlink/?linkid=2006060" rel="noopener noreferrer">IntelliCode Extension for Visual Studio Code</a>. IntelliCode saves you time by putting the most relevant suggestions at the top of your completion list. IntelliCode recommendations are based on thousands of open source projects on GitHub, each with over 100 stars, so it’s trained on most popular usage patterns and practices. When combined with the context of your code, the completion list is tailored to promote those practices. Check out the animation below to see IntelliCode for Java in action. <img width="1024" height="768" class="alignnone size-full wp-image-216805" alt="IntelliCode for Java" src="https://devblogs72.wpengine.com/visualstudio/wp-content/uploads/sites/4/2018/11/intellicode_4_a.gif" /> You may have noticed that IntelliCode provides most relevant IntelliSense recommendations based on your current code context, especially within conditional blocks. IntelliCode works well with popular Java libraries and frameworks like Java SE platform and Spring framework. It will help you whether you are doing monolithic or modern microservices architecture. 
## Exploring and managing your Java project You speak, we listen. Some of the most frequent feedback requests we received from developers on Visual Studio Code are the lack of a package view, dependency management and project creation. Thus, we’ve built a new extension to provide those features – 

<a target="_blank" href="https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-dependency" rel="noopener noreferrer">Java Dependencies</a>. See below for package and dependency view. <img width="1024" height="768" class="alignnone wp-image-216777 size-full" alt="Package and Dependency Viewer" src="https://devblogs72.wpengine.com/visualstudio/wp-content/uploads/sites/4/2018/11/2018.11.12.PackageViewer.gif" /> And create a simple Java project. <img width="1024" height="768" class="alignnone wp-image-216778 size-full" alt="Create Java project" src="https://devblogs72.wpengine.com/visualstudio/wp-content/uploads/sites/4/2018/11/2018.11.12.CreateProject.gif" /> 
## Spring Tool 4 available for Visual Studio Code During 

<a target="_blank" href="https://springoneplatform.io/" rel="noopener noreferrer">SpringOne 2018</a>, Pivotal announced the release of their brand new <a target="_blank" href="https://spring.io/tools" rel="noopener noreferrer">Spring Tool 4</a> built on top of the Language Server Protocol developed by Visual Studio Code team, and it’s now available for Visual Studio Code, Eclipse and Atom. Pivotal and Microsoft presented sessions to promote that during both <a target="_blank" href="https://springoneplatform.io/" rel="noopener noreferrer">SpringOne</a> and <a target="_blank" href="https://www.oracle.com/code-one/index.html" rel="noopener noreferrer">Oracle Code One</a>. Along with <a target="_blank" href="https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-spring-initializr" rel="noopener noreferrer">Spring Initializr</a> and <a target="_blank" href="https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-spring-boot-dashboard" rel="noopener noreferrer">Spring Boot Dashboard</a>, now you can easily create new Spring Boot applications, navigate your source code, have smart code editing, see runtime live information in your editor and manage your running application, all within Visual Studio Code. <img width="1024" height="768" class="alignnone size-full wp-image-216788" alt="Spring Tools 4" src="https://devblogs72.wpengine.com/visualstudio/wp-content/uploads/sites/4/2018/11/sts4_4_a.gif" /> View the recording of <a target="_blank" href="https://springoneplatform.io/2018/sessions/hacking-spring-boot-applications-using-visual-studio-code" rel="noopener noreferrer">Hacking Spring Boot Applications Using Visual Studio Code</a> to learn more. 
## More improvements for Java in Visual Studio Code There’s also lots of additional new features added to our Java on Visual Studio Code extension lineup, including 

<a target="_blank" href="https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-debug" rel="noopener noreferrer">Debugger for Java</a> 
1.  Use code lens to run Java program in a much simpler way.
2.  Add support for <a target="_blank" href="https://code.visualstudio.com/blogs/2018/07/12/introducing-logpoints-and-auto-attach" rel="noopener noreferrer">Logpoints</a>.
3.  Add a troubleshooting page for common errors.
4.  Support starting without debugging.
5.  Add new user settings java.debug.settings.enableRunDebugCodeLens to enable/disable Run|Debug Code Lenses on main methods <a target="_blank" href="https://github.com/Microsoft/vscode-java-debug/issues/464" rel="noopener noreferrer">#464</a> (Thank you <a target="_blank" href="https://github.com/ThadHouse" rel="noopener noreferrer">Thad House</a>!)
6.  Add Italian translation for extension configuration <a target="_blank" href="https://github.com/Microsoft/vscode-java-debug/pull/463" rel="noopener noreferrer">#463</a> (Thank you <a target="_blank" href="https://github.com/Dotpys" rel="noopener noreferrer">Julien Russo</a>!)

<a target="_blank" href="https://marketplace.visualstudio.com/items?itemName=adashen.vscode-tomcat" rel="noopener noreferrer">Tomcat</a> 
1.  Support right click on exploded WAR folder to run it directory Tomcat Server
2.  Support right click on exploded WAR folder to debug it directory on Tomcat Server
3.  Add command "Generate WAR Package from Current Folder"

<a target="_blank" href="https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-maven" rel="noopener noreferrer">Maven</a> 
1.  Supported to fast re-run maven command from history. Added entry for historical commands in context menu.
2.  Supported to trigger maven command from command palette.
3.  Supported to hide Maven explorer view by default.
4.  Started to use a separate terminal for each root folder.
5.  Supported to update explorer automatically when workspace folders change. With the help from 

<a target="_blank" href="https://marketplace.visualstudio.com/items?itemName=redhat.java" rel="noopener noreferrer">Language Support for Java by Red Hat</a>, we now have better support for newer versions of Java (9, 10, and 11), better integrations with the editor (outline, go to implementation), more code actions (convert var to type and vice versa, convert to lambda expression) and various other enhancements. 
## Provide feedback Your feedback and suggestions are especially important to us and will help shape our products in future. Please help us by taking this 

<a target="_blank" href="https://www.research.net/r/vscodejava-blog?o=%5bo_value%5d&m=%5bm_value%5d" rel="noopener noreferrer">survey</a> to share your thoughts! 
## Try it out Please don’t hesitate to have a try on using Visual Studio Code for your Java development and let us know your feelings! Visual Studio Code is a lightweight and performant code editor with great Java support especially for building microservices. Install the 

<a target="_blank" href="https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-pack" rel="noopener noreferrer">Java Extension Pack</a> which including <a target="_blank" href="https://marketplace.visualstudio.com/items?itemName=redhat.java" rel="noopener noreferrer">Language Support for Java™ by Red Hat</a>, <a target="_blank" href="https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-debug" rel="noopener noreferrer">Debugger for Java</a>, <a target="_blank" href="https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-maven" rel="noopener noreferrer">Maven</a> and <a target="_blank" href="https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-test" rel="noopener noreferrer">Java Test Runner</a>. 
*   Install <a target="_blank" href="https://go.microsoft.com/fwlink/?linkid=2006060" rel="noopener noreferrer">IntelliCode Extension for Visual Studio Code</a> to try out the AI-assisted IntelliSense.
*   Install other Java related extensions base on your needs, including 
    *   Checkout <a target="_blank" href="https://marketplace.visualstudio.com/items?itemName=adashen.vscode-tomcat" rel="noopener noreferrer">Tomcat</a> and <a target="_blank" href="https://marketplace.visualstudio.com/items?itemName=SummerSun.vscode-jetty" rel="noopener noreferrer">Jetty</a> if you’re working with those technologies.
    *   In case you’re working on Spring Boot, there’re also great support provided by <a target="_blank" href="https://marketplace.visualstudio.com/items?itemName=Pivotal.vscode-boot-dev-pack" rel="noopener noreferrer">Pivotal</a> and <a target="_blank" href="https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-spring-initializr" rel="noopener noreferrer">Microsoft</a> available on Visual Studio Code including <a target="_blank" href="https://marketplace.visualstudio.com/items?itemName=Pivotal.vscode-spring-boot" rel="noopener noreferrer">Spring Boot Tools</a>, <a target="_blank" href="https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-spring-initializr" rel="noopener noreferrer">Spring Initializr</a> and <a target="_blank" href="https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-spring-boot-dashboard" rel="noopener noreferrer">Spring Boot Dashboard</a>.
    *   <a target="_blank" href="https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-dependency" rel="noopener noreferrer">Java Dependencies</a> provides you a package view of your Java project and helps you managing your dependencies.
    *   <a target="_blank" href="https://marketplace.visualstudio.com/items?itemName=shengchen.vscode-checkstyle" rel="noopener noreferrer">Checkstyle</a> could be handy when you need coherence code style especially cross multiple team members.
*   Learn more about <a target="_blank" href="https://code.visualstudio.com/docs/languages/java" rel="noopener noreferrer">Java on Visual Studio Code</a>.
*   Explore our step by step <a target="_blank" href="https://code.visualstudio.com/docs/java/java-tutorial" rel="noopener noreferrer">Java Tutorials on Visual Studio Code</a>.