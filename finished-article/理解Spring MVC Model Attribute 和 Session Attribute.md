<p>作为一名 Java Web 应用开发者，你已经快速学习了 request（HttpServletRequest）和 session（HttpSession）作用域。在设计和构建 Java Web 应用时，理解这些作用域，如何将数据与对象和这些作用域交互是十分重要的。【在 StackOverflow 上有一篇<a class="external" href="http://stackoverflow.com/questions/3106452/how-do-servlets-work-instantiation-session-variables-and-multithreading/3106909#3106909" rel="nofollow" target="_blank">文章</a>可以帮助你快速了解 request 和 session 作用域】</p>
<h3>SPRING MVC 作用域</h3>
<p>当我开始用 Spring MVC 编写 Web 应用时，我发现 Spring model 和 session attribute 有一点神秘，尤其当它们与我熟知的 HTTP request 和 session 作用域交互时。一个 Spring model 元素可以从我的 session 或者 request 中找到吗？如果是这样的话，我该如何控制？在这篇文章中，我希望讲解清楚 Spring MVC 的 model 与 session 是如何工作的。</p>
<h3>SPRING 的 @MODELATTRIBUTE</h3>
<p>有几种方法将数据或对象添加到 Spring 的 model 中。一般来说，数据或对象是通过 controller 层的一个注解添加进 Spring 的 model 中。在下面的例子中，使用 @ModelAttribute 添加一个名为 MyCommandBean 的实例给 key 值为『myRequestObject』的 model。</p>
<div class="cnblogs_code">
<pre><span style="color: #008080;"> 1</span> <span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span><span style="color: #000000;"> MyController {
</span><span style="color: #008080;"> 2</span>  
<span style="color: #008080;"> 3</span>     @ModelAttribute("myRequestObject"<span style="color: #000000;">)
</span><span style="color: #008080;"> 4</span>     <span style="color: #0000ff;">public</span><span style="color: #000000;"> MyCommandBean addStuffToRequestScope() {
</span><span style="color: #008080;"> 5</span>         System.out.println("Inside of addStuffToRequestScope"<span style="color: #000000;">);
</span><span style="color: #008080;"> 6</span>         MyCommandBean bean = <span style="color: #0000ff;">new</span> MyCommandBean("Hello World",42<span style="color: #000000;">);
</span><span style="color: #008080;"> 7</span>         <span style="color: #0000ff;">return</span><span style="color: #000000;"> bean;
</span><span style="color: #008080;"> 8</span> <span style="color: #000000;">    }
</span><span style="color: #008080;"> 9</span>  
<span style="color: #008080;">10</span>     @RequestMapping("/dosomething"<span style="color: #000000;">)
</span><span style="color: #008080;">11</span>     <span style="color: #0000ff;">public</span><span style="color: #000000;"> String requestHandlingMethod(Model model, HttpServletRequest request) {
</span><span style="color: #008080;">12</span>         System.out.println("Inside of dosomething handler method"<span style="color: #000000;">);
</span><span style="color: #008080;">13</span>  
<span style="color: #008080;">14</span>         System.out.println("--- Model data ---"<span style="color: #000000;">);
</span><span style="color: #008080;">15</span>         Map modelMap =<span style="color: #000000;"> model.asMap();
</span><span style="color: #008080;">16</span>         <span style="color: #0000ff;">for</span><span style="color: #000000;"> (Object modelKey : modelMap.keySet()) {
</span><span style="color: #008080;">17</span>             Object modelValue =<span style="color: #000000;"> modelMap.get(modelKey);
</span><span style="color: #008080;">18</span>             System.out.println(modelKey + " -- " +<span style="color: #000000;"> modelValue);
</span><span style="color: #008080;">19</span> <span style="color: #000000;">        }
</span><span style="color: #008080;">20</span>  
<span style="color: #008080;">21</span>         System.out.println("=== Request data ==="<span style="color: #000000;">);
</span><span style="color: #008080;">22</span>         java.util.Enumeration reqEnum =<span style="color: #000000;"> request.getAttributeNames();
</span><span style="color: #008080;">23</span>         <span style="color: #0000ff;">while</span><span style="color: #000000;"> (reqEnum.hasMoreElements()) {
</span><span style="color: #008080;">24</span>             String s =<span style="color: #000000;"> reqEnum.nextElement();
</span><span style="color: #008080;">25</span> <span style="color: #000000;">            System.out.println(s);
</span><span style="color: #008080;">26</span>             System.out.println("==" +<span style="color: #000000;"> request.getAttribute(s));
</span><span style="color: #008080;">27</span> <span style="color: #000000;">        }
</span><span style="color: #008080;">28</span>  
<span style="color: #008080;">29</span>         <span style="color: #0000ff;">return</span> "nextpage"<span style="color: #000000;">;
</span><span style="color: #008080;">30</span> <span style="color: #000000;">    }
</span><span style="color: #008080;">31</span>  
<span style="color: #008080;">32</span>          <span style="color: #008000;">//</span><span style="color: #008000;">  ... the rest of the controller</span>
<span style="color: #008080;">33</span> }</pre>
</div>
<p>在一个到达的 request 中，任何被 @ModelAttribute 注解的方法都会在 controller handler method 之前调用（就像上面例子中的 requestHandlingMethod 一样）。这些方法会赶在 handler method 执行之前将数据添加进一个 java.util.Map，然后加入 Spring model 中。可以用一个示例操作展示出来。我创建了两个 JSP 页面：index.jsp 和 nextpage.jsp。index.jsp 上的一个链接用于向 MyController 中的 requestHandlingMethod() 应用触发器发送一个 request。上面的代码中，requestHandlingMethod() 将『nextpage』作为下个视图的逻辑名返回，其在这个例子中会处理为 nextpage.jsp。</p>
<p><img src="http://ww2.sinaimg.cn/mw690/b254dc71jw1ewwctqhslaj207e01d0sn.jpg" alt="" /></p>
<p>当这个小小的网址被修改为这种形式后，controller 的 System.out.println 展现了 @ModelAttribute 方法是如何在 handler method 之前执行的。同时也展现了 MyCommandBean 创建和加入 Spring model，并在 handler method 中可用的过程。</p>
<div>
<div id="highlighter_942480" class="syntaxhighlighter notranslate java">
<div class="cnblogs_code">
<pre><span style="color: #008080;"> 1</span> <span style="color: #000000;">Inside of addStuffToRequestScope
</span><span style="color: #008080;"> 2</span> <span style="color: #000000;">Inside of dosomething handler method
</span><span style="color: #008080;"> 3</span> --- Model data ---
<span style="color: #008080;"> 4</span> myRequestObject -- MyCommandBean [someString=Hello World, someNumber=42<span style="color: #000000;">]
</span><span style="color: #008080;"> 5</span> === Request data ===
<span style="color: #008080;"> 6</span> <span style="color: #000000;">org.springframework.web.servlet.DispatcherServlet.THEME_SOURCE
</span><span style="color: #008080;"> 7</span> ==WebApplicationContext <span style="color: #0000ff;">for</span> namespace 'dispatcher-servlet': startup date [Sun Oct 13 21:40:56 CDT 2013<span style="color: #000000;">]; root of context hierarchy
</span><span style="color: #008080;"> 8</span> <span style="color: #000000;">org.springframework.web.servlet.DispatcherServlet.THEME_RESOLVER
</span><span style="color: #008080;"> 9</span> ==<span style="color: #000000;">org.springframework.web.servlet.theme.FixedThemeResolver@204af48c
</span><span style="color: #008080;">10</span> <span style="color: #000000;">org.springframework.web.servlet.DispatcherServlet.CONTEXT
</span><span style="color: #008080;">11</span> ==WebApplicationContext <span style="color: #0000ff;">for</span> namespace 'dispatcher-servlet': startup date [Sun Oct 13 21:40:56 CDT 2013<span style="color: #000000;">]; root of context hierarchy
</span><span style="color: #008080;">12</span> <span style="color: #000000;">org.springframework.web.servlet.HandlerMapping.pathWithinHandlerMapping
</span><span style="color: #008080;">13</span> ==<span style="color: #000000;">dosomething.request
</span><span style="color: #008080;">14</span> <span style="color: #000000;">org.springframework.web.servlet.HandlerMapping.bestMatchingPattern
</span><span style="color: #008080;">15</span> ==/dosomething.*
<span style="color: #008080;">16</span> <span style="color: #000000;">org.springframework.web.servlet.DispatcherServlet.LOCALE_RESOLVER
</span><span style="color: #008080;">17</span> ==org.springframework.web.servlet.i18n.AcceptHeaderLocaleResolver@18fd23e4</pre>
</div>
</div>
</div>
<p>现在问题变为了『Spring model 的数据存储在哪里？』是存储在标准 Java request 作用域中么？答案是 &mdash;&mdash; 对的。。。就最终而言的话。就像你从上面的输出中读到的，MyCommandBean 在 model 中，但当 handler method 执行时还不在 request 对象中。的确，handler method 执行之后，下个视图（本例中为 nextpage.jsp）显示之前为止，Spring 都没有将 model 数据作为 attribute 加入 request 中。</p>
<p><img src="http://ww4.sinaimg.cn/mw690/b254dc71jw1ewwctr1t0oj207v03raa8.jpg" alt="" /></p>
<p>也可以通过输出存储在 index.jsp 与 nextpage.jsp 的 HttpServletRequest 中的 attribute 展现出来。我在两个页面中都布置了一个 JSP 代码块（如下面所示），用以展现 HttpServletRequest 的 attribute。</p>
<div>
<div id="highlighter_927587" class="syntaxhighlighter notranslate java">
<div class="cnblogs_code">
<pre><span style="color: #008080;"> 1</span> &lt;HR /&gt;
<span style="color: #008080;"> 2</span> &lt;H3&gt;REQUEST SCOPE (KEY==VALUES)&lt;/H3&gt;
<span style="color: #008080;"> 3</span> &lt;%
<span style="color: #008080;"> 4</span>     JAVA.UTIL.ENUMERATION&lt;STRING&gt; REQENUM =<span style="color: #000000;"> REQUEST.GETATTRIBUTENAMES();
</span><span style="color: #008080;"> 5</span> <span style="color: #000000;">    WHILE (REQENUM.HASMOREELEMENTS()) {
</span><span style="color: #008080;"> 6</span>         STRING S =<span style="color: #000000;"> REQENUM.NEXTELEMENT();
</span><span style="color: #008080;"> 7</span> <span style="color: #000000;">        OUT.PRINT(S);
</span><span style="color: #008080;"> 8</span>         OUT.PRINTLN("==" +<span style="color: #000000;"> REQUEST.GETATTRIBUTE(S));
</span><span style="color: #008080;"> 9</span> %&gt;&lt;BR /&gt;
<span style="color: #008080;">10</span> &lt;%
<span style="color: #008080;">11</span> <span style="color: #000000;">    }
</span><span style="color: #008080;">12</span> %&gt;</pre>
</div>
</div>
</div>
<p>当应用启动，index.jsp 加载完毕，你可以看到在 request 作用域中没有 attribute。</p>
<p><a class="external cboxElement" title="理解Spring MVC Model Attribute 和 Session Attribute" href="http://jbcdn2.b0.upaiyun.com/2015/06/8fc5445cc167a235a76cf49d3def58ae.png" rel="lightbox[16782] nofollow" target="_blank"><img class="alignnone size-full wp-image-38130" src="http://jbcdn2.b0.upaiyun.com/2015/06/8fc5445cc167a235a76cf49d3def58ae.png" alt="requestattributesbefore" width="261" height="87" /></a></p>
<p>在本例中，当『do something』被点击时执行 MyController 的 handler method，然后会跳转并展示 nextpage.jsp。而 nextpage.jsp 中已经编写了相同的 JSP 代码块，同样提供了 request 作用域中的 attribute。瞧，当 nextpage.jsp 渲染后，显示出在 controller 中创建的 MyCommandBean model 被加进 HttpServletRequest 作用域中了！Spring model attribute 的键值『myRequestObject』被复制后用作 request attribute 的键值。</p>
<p><img src="http://ww2.sinaimg.cn/mw690/b254dc71jw1ewwctrnpugj208c03a74m.jpg" alt="" /></p>
<p>所以下一个视图呈现之前，Spring model 数据已经在 handler method 执行之前（或者之间）被拷贝给了 HttpServletRequest。</p>
<h3>使用 SPRING MODEL 与 REQUEST 的原因</h3>
<p>你或许想知道为什么 Spring 使用 model attribute。为何不直接把数据加到 request 对象里？我在 Rod Johnson 等人的书籍<a class="external" href="http://www.amazon.com/Professional-Java-Development-Spring-Framework/dp/0764574833" rel="nofollow" target="_blank">《Professional Java Development with the Spring Framework》</a>中找到了答案。这本书关于 Spring API 的部分有一点过时（基于 Spring 2.0 编写），但是我发现该书提供了一些对于 Spring 引擎运行的扩展解释。下面是书中 model 元素部分的引用：</p>
<blockquote>
<p>直接将元素加入 HttpServletRequest（像 request attributes 一样）看起来就像在服务同样的目标。这样做的理由是当看到我们为 MVC 框架设置的 requirements 时，能够更明确。它应尽可能与视图无关，这意味着我们可以合并视图技术，并不受 HttpServletRequest 的束缚。</p>
</blockquote>
<h3>SPRING 的 @SESSIONATTRIBUTES</h3>
<p>所以现在你知道了 Spring 如何管理 model 数据，与如何连接标准的 Http request attribute 数据。那么关于 Spring 的 session 数据呢？</p>
<p>Spring 的 @SessionAttribute 在 controller 中用来指定哪一个 model attributes 需要存储到 session。事实上，<a class="external" href="http://docs.spring.io/spring/docs/3.1.4.RELEASE/javadoc-api/org/springframework/web/bind/annotation/SessionAttributes.html" rel="nofollow" target="_blank">Spring 文档</a>声明了 @SessionAttributes 注解『列举需要显式地存储 session 或一些交互用的存储空间内的 model attributes 名称。』另外说一下，『一些交互存储空间』表明了 Spring MVC 试图保持与技术无关联的设计思想。</p>
<p>事实上，@SessionAttributes 允许你做的就是告诉 Spring 哪一个 model attributes 将在视图展现之前一同拷贝给 HttpSession。关于这一点同样可以用一个简短的代码来展示。</p>
<p>在 index.jsp 和 nextpage.jsp 中，我添加了额外的 JSP 代码块，使其显示 HttpSession attributes。</p>
<div>
<div id="highlighter_558913" class="syntaxhighlighter notranslate java">
<div class="cnblogs_code">
<pre><span style="color: #008080;"> 1</span> &lt;H3&gt;SESSION SCOPE (KEY==VALUES)&lt;/H3&gt;
<span style="color: #008080;"> 2</span> &lt;%
<span style="color: #008080;"> 3</span>   JAVA.UTIL.ENUMERATION&lt;STRING&gt; SESSENUM =<span style="color: #000000;"> REQUEST.GETSESSION()
</span><span style="color: #008080;"> 4</span> <span style="color: #000000;">    .GETATTRIBUTENAMES();
</span><span style="color: #008080;"> 5</span> <span style="color: #000000;">  WHILE (SESSENUM.HASMOREELEMENTS()) {
</span><span style="color: #008080;"> 6</span>     STRING S =<span style="color: #000000;"> SESSENUM.NEXTELEMENT();
</span><span style="color: #008080;"> 7</span> <span style="color: #000000;">    OUT.PRINT(S);
</span><span style="color: #008080;"> 8</span>     OUT.PRINTLN("==" +<span style="color: #000000;"> REQUEST.GETSESSION().GETATTRIBUTE(S));
</span><span style="color: #008080;"> 9</span> %&gt;&lt;BR /&gt;
<span style="color: #008080;">10</span> &lt;%
<span style="color: #008080;">11</span> <span style="color: #000000;">  }
</span><span style="color: #008080;">12</span> %&gt;</pre>
</div>
</div>
</div>
<p>我使用 @SessionAttributes 注解 MyController，使其将同一个 model attributes（myRequestObject）放入 Spring session 中。</p>
<div>
<div id="highlighter_202830" class="syntaxhighlighter notranslate java">
<div class="cnblogs_code">
<pre><span style="color: #008080;">1</span> <span style="color: #000000;">@CONTROLLER
</span><span style="color: #008080;">2</span> @SESSIONATTRIBUTES("MYREQUESTOBJECT"<span style="color: #000000;">)
</span><span style="color: #008080;">3</span> <span style="color: #000000;">PUBLIC CLASS MYCONTROLLER {
</span><span style="color: #008080;">4</span> <span style="color: #000000;">  ...
</span><span style="color: #008080;">5</span> }</pre>
</div>
</div>
</div>
<p>另外在 controller 的 handler method 中添加代码显示 HttpSession 中的 attributes（就像显示 HttpServletRequest 中的 attributes 一样）。</p>
<div>
<div id="highlighter_995205" class="syntaxhighlighter notranslate java">
<div class="cnblogs_code">
<pre><span style="color: #008080;"> 1</span> @SUPPRESSWARNINGS("RAWTYPES"<span style="color: #000000;">)
</span><span style="color: #008080;"> 2</span> @REQUESTMAPPING("/DOSOMETHING"<span style="color: #000000;">)
</span><span style="color: #008080;"> 3</span> <span style="color: #000000;">PUBLIC STRING REQUESTHANDLINGMETHOD(MODEL MODEL, HTTPSERVLETREQUEST REQUEST, HTTPSESSION SESSION) {
</span><span style="color: #008080;"> 4</span>   SYSTEM.OUT.PRINTLN("INSIDE OF DOSOMETHING HANDLER METHOD"<span style="color: #000000;">);
</span><span style="color: #008080;"> 5</span> 
<span style="color: #008080;"> 6</span>   SYSTEM.OUT.PRINTLN("--- MODEL DATA ---"<span style="color: #000000;">);
</span><span style="color: #008080;"> 7</span>   MAP MODELMAP =<span style="color: #000000;"> MODEL.ASMAP();
</span><span style="color: #008080;"> 8</span> <span style="color: #000000;">  FOR (OBJECT MODELKEY : MODELMAP.KEYSET()) {
</span><span style="color: #008080;"> 9</span>     OBJECT MODELVALUE =<span style="color: #000000;"> MODELMAP.GET(MODELKEY);
</span><span style="color: #008080;">10</span>     SYSTEM.OUT.PRINTLN(MODELKEY + " -- " +<span style="color: #000000;"> MODELVALUE);
</span><span style="color: #008080;">11</span> <span style="color: #000000;">  }
</span><span style="color: #008080;">12</span> 
<span style="color: #008080;">13</span>   SYSTEM.OUT.PRINTLN("=== REQUEST DATA ==="<span style="color: #000000;">);
</span><span style="color: #008080;">14</span>   JAVA.UTIL.ENUMERATION&lt;STRING&gt; REQENUM =<span style="color: #000000;"> REQUEST.GETATTRIBUTENAMES();
</span><span style="color: #008080;">15</span> <span style="color: #000000;">  WHILE (REQENUM.HASMOREELEMENTS()) {
</span><span style="color: #008080;">16</span>     STRING S =<span style="color: #000000;"> REQENUM.NEXTELEMENT();
</span><span style="color: #008080;">17</span> <span style="color: #000000;">    SYSTEM.OUT.PRINTLN(S);
</span><span style="color: #008080;">18</span>     SYSTEM.OUT.PRINTLN("==" +<span style="color: #000000;"> REQUEST.GETATTRIBUTE(S));
</span><span style="color: #008080;">19</span> <span style="color: #000000;">  }
</span><span style="color: #008080;">20</span> 
<span style="color: #008080;">21</span>   SYSTEM.OUT.PRINTLN("*** SESSION DATA ***"<span style="color: #000000;">);
</span><span style="color: #008080;">22</span>   ENUMERATION&lt;STRING&gt; E =<span style="color: #000000;"> SESSION.GETATTRIBUTENAMES();
</span><span style="color: #008080;">23</span> <span style="color: #000000;">  WHILE (E.HASMOREELEMENTS()){
</span><span style="color: #008080;">24</span>     STRING S =<span style="color: #000000;"> E.NEXTELEMENT();
</span><span style="color: #008080;">25</span> <span style="color: #000000;">    SYSTEM.OUT.PRINTLN(S);
</span><span style="color: #008080;">26</span>     SYSTEM.OUT.PRINTLN("**" +<span style="color: #000000;"> SESSION.GETATTRIBUTE(S));
</span><span style="color: #008080;">27</span> <span style="color: #000000;">  }
</span><span style="color: #008080;">28</span> 
<span style="color: #008080;">29</span>   RETURN "NEXTPAGE"<span style="color: #000000;">;
</span><span style="color: #008080;">30</span> }</pre>
</div>
</div>
</div>
<p>现在，我们可以看见加上 @SessionAttributes 注解后，Spring MVC 处理一个 HTTP 请求之前、之间和之后的 session 对象情况。下面显示了结果。首先，当 index.jsp 显示时（请求被 Spring MVC 发送和处理之前），我们可以看见 HttpServletRequest 和 HttpSession 都没有 attribute 数据。</p>
<p><a class="external cboxElement" title="理解Spring MVC Model Attribute 和 Session Attribute" href="http://jbcdn2.b0.upaiyun.com/2015/06/07b5a339bfd18b6200857ee0f60cf098.png" rel="lightbox[16782] nofollow" target="_blank"><img class="alignnone size-medium wp-image-38132" src="http://jbcdn2.b0.upaiyun.com/2015/06/07b5a339bfd18b6200857ee0f60cf098-300x154.png" alt="before-request-attribute-list" width="300" height="154" /></a></p>
<p>handler method 执行时（requestHandlingMethod），你可以看见 MyCommandBean 被添加进 Spring model attributes，但是还没有加入 HttpServletRequest 或 HttpSession 作用域。</p>
<p><img src="http://ww4.sinaimg.cn/mw690/b254dc71jw1ewwctsljq1j208c04dwfc.jpg" alt="" /></p>
<p>但是 handler method 执行后和 nextpage.jsp 显示时，你可以看见 model attribute 数据（MyCommandBean）已经作为一个 attribute 被复制给了 HttpServletRequest 和 HttpSession（拥有相同的 attribute key）。</p>
<p><img src="http://ww3.sinaimg.cn/mw690/b254dc71jw1ewwcttq4rsj208c04c74x.jpg" alt="" /></p>
<h3>控制 SESSION ATTRIBUTES</h3>
<p>现在你已经理解了 Spring model 和 session attribute 数据如何添加进 HttpServletRequest 与 HttpSession。或许又开始关心怎么管理 Spring session 中的数据。Spring 提供了一个方法移除 Spring session attributes，同时也会从 HttpSession 中移除（不需要删除整个 HttpSession）。简单地将一个 Spring SessionStatus 对象作为参数加入一个 controller handler method 中。在此方法中，使用 SessionStatus 对象结束这个 Spring session。</p>
<div>
<div id="highlighter_394261" class="syntaxhighlighter notranslate java">
<div class="cnblogs_code">
<pre><span style="color: #008080;">1</span> @REQUESTMAPPING("/ENDSESSION"<span style="color: #000000;">)
</span><span style="color: #008080;">2</span> <span style="color: #000000;">PUBLIC STRING NEXTHANDLINGMETHOD2(SESSIONSTATUS STATUS){
</span><span style="color: #008080;">3</span> <span style="color: #000000;">  STATUS.SETCOMPLETE();
</span><span style="color: #008080;">4</span>   RETURN "LASTPAGE"<span style="color: #000000;">;
</span><span style="color: #008080;">5</span> }</pre>
</div>
</div>
</div>
<h3>总结</h3>
<p>希望这篇文章能够帮助你理解 Spring model 和 session attributes。这并不神奇，仅仅是一个理解 HttpSession 和 HttpServletRequest 如何存储 Spring model 和 session attributes 的问题。我已经将展示用的代码放在了 Intertech Web site 上。如果你对继续探索与理解 Spring model 和 session 感兴趣，尽管从<a class="external" href="http://www.intertech.com/downloads/SessionTest.zip" rel="nofollow" target="_blank">这里</a>下载吧。</p>
<p>如果你对深入学习 Spring（或任何一种 Java 技术）感兴趣，可以考虑马上注册，成为 Intertech 的一员。在<a class="external" href="http://www.intertech.com/Training/Java/Frameworks/Spring" rel="nofollow" target="_blank">这里</a>学到更多与注册。</p>
<hr />
<p>原文链接：&nbsp;<a class="external" href="http://www.intertech.com/Blog/understanding-spring-mvc-model-and-session-attributes/" rel="nofollow" target="_blank">Intertech</a><br />首发于 importnew，译文链接：&nbsp;<a href="http://www.importnew.com/16782.html">http://www.importnew.com/16782.html</a></p>