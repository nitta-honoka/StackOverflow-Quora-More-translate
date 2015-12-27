<h3>导读</h3>
<p>本文来自stackoverflow的问答，讨论了Java Servlet的工作机制，如何进行实例化、共享变量和多线程处理。</p>
<h3>问题：Servlet 是如何工作的？Servlet 如何实例化、共享变量、并进行多线程处理？</h3>
<p>假设我有一个运行了大量&nbsp;<code>Servlet</code>&nbsp;的 web 服务器。通过&nbsp;<code>Servlet</code>&nbsp;之间传输信息得到&nbsp;<code>Servlet</code>&nbsp;上下文，并设置 session 变量。</p>
<p>现在，如果有两名或更多使用者向这个服务发送请求，接下来 session 变量会发生什么变化？究竟是所有用户都是用共同的变量？还是不同的用户使用的变量都不一样？如果是后者，服务器如何区分不同用户？</p>
<p>另一个相似的问题，如果有&nbsp;<code>*n*</code>&nbsp;名用户访问一个特定的&nbsp;<code>Servlet</code>，那么该&nbsp;<code>Servlet</code>&nbsp;是仅在第一个用户首次访问的时候实例化，还是分别为每个用户实例化？</p>
<h3>回答（BalusC）：</h3>
<h4>ServletContext</h4>
<p>当 Servlet 容器（比如&nbsp;<a class="external" href="http://tomcat.apache.org/" rel="nofollow" target="_blank">Apache Tomcat</a>）启动后，会部署和加载所有 web 应用。当web 应用被加载，Servlet 容器会创建一次&nbsp;<a class="external" href="http://docs.oracle.com/javaee/7/api/javax/servlet/ServletContext.html" rel="nofollow" target="_blank"><code>ServletContext</code></a>，然后将其保存在服务器的内存中。web 应用的&nbsp;<code>web.xml</code>&nbsp;被解析，找到其中所有&nbsp;<code>servlet</code>、<code>filter</code>&nbsp;和&nbsp;<code>Listener</code>&nbsp;或&nbsp;<code>@WebServlet</code>、<code>@WebFilter</code>&nbsp;和&nbsp;<code>@WebListener</code>&nbsp;注解的内容，创建一次并保存到服务器的内存中。对于所有过滤器会立即调用&nbsp;<code>init()</code>。当 Servlet 容器停止，将卸载所有 web 应用，调用所有初始化的 Servlet 和过滤器的&nbsp;<code>destroy()</code>&nbsp;方法，最后回收&nbsp;<code>ServletContext</code>&nbsp;和所有&nbsp;<code>Servlet</code>、Filter 与&nbsp;<code>Listener</code>&nbsp;实例。</p>
<p>当问题中的&nbsp;<code>Servlet</code>&nbsp;配置的&nbsp;<code>load-on-startup</code>&nbsp;或者&nbsp;<code>@WebServlet(loadOnStartup)</code>&nbsp;设置了一个大于 0 的值，则同样会在启动的时候立即调用&nbsp;<code>init()</code>&nbsp;方法。&ldquo;load-on-startup&rdquo;中的值表示那些 Servlet 会以相同顺序初始化。如果配置的值相同，会遵循&nbsp;<code>web.xml</code>&nbsp;中指定的顺序或<code>@WebServlet</code>&nbsp;类加载的顺序。另外，如果不设置 &ldquo;load-on-startup&rdquo; 值，<code>init()</code>&nbsp;方法只在第一次 HTTP 请求命中问题中的 Servlet 时才被调用。</p>
<h4>HttpServletRequest 与 HttpServletResponse</h4>
<p>Servlet 容器附加在一个 web 服务上，这个 web 服务会在某个端口号上监听 HTTP 请求，在开发环境中这个端口通常为 8080，生产环境中通常为 80。当客户端（web 浏览器）发送了一个 HTTP 请求，Servlet 容器会创建新的&nbsp;<a class="external" href="http://docs.oracle.com/javaee/7/api/javax/servlet/http/HttpServletRequest.html" rel="nofollow" target="_blank"><code>HttpServletRequest</code></a>&nbsp;和&nbsp;<a class="external" href="http://docs.oracle.com/javaee/7/api/javax/servlet/http/HttpServletResponse.html" rel="nofollow" target="_blank"><code>HttpServletResponse</code></a>&nbsp;对象，传递给已创建好并且请求的 URL 匹配&nbsp;<code>url-pattern</code>&nbsp;的&nbsp;<code>Filter</code>&nbsp;和&nbsp;<code>Servlet</code>&nbsp;实例中的方法，所有工作都在同一个线程中处理。</p>
<p>request 对象可以访问所有该 HTTP 请求中的信息，例如 request header 和 request body。response 对象为你提供需要的控制和发送 HTTP 响应方法，例如设置 header 和 body（通常会带有 JSP 文件中的 HTML 内容）。提交并完成HTTP 响应后，将回收 request 和 response 对象。</p>
<h4>HttpSession</h4>
<p>当用户第一次访问该 web 应用时，会通过&nbsp;<code>request.getSession()</code>&nbsp;第一次获得&nbsp;<a class="external" href="http://docs.oracle.com/javaee/7/api/javax/servlet/http/HttpSession.html" rel="nofollow" target="_blank">HttpSession</a>。之后 Servlet 容器将会创建&nbsp;<code>HttpSession</code>，生成一个唯一的 ID（可以通过&nbsp;<code>session.getId()</code>&nbsp;获取）并储存在服务器内存中。然后 Servlet 容器在该次 HTTP 响应的&nbsp;<code>Set-Cookie</code>&nbsp;头部设置一个<a class="external" href="http://docs.oracle.com/javaee/7/api/javax/servlet/http/Cookie.html" rel="nofollow" target="_blank"><code>Cookie</code></a>，以&nbsp;<code>JSESSIONID</code>&nbsp;作为 Cookie 名字，那个唯一的 session ID 作为&nbsp;<code>Cookie</code>&nbsp;的值。</p>
<p>按照&nbsp;<a class="external" href="http://www.faqs.org/rfcs/rfc2965.html" rel="nofollow" target="_blank">HTTP cookie 规则</a>（正常 web 浏览器和 web 服务端必须遵循的标准），当 cookie 有效时，要求客户端（浏览器）在后续请求的&nbsp;<code>Cookie</code>&nbsp;头中返回这个 cookie。使用浏览器内置的 HTTP 流量监控器，你可以查看它们（在 Chrome、Firefox23+、IE9+ 中按 F12，然后查看 Net/Network 标签）。Servlet 容器将会确定每个进入的 HTTP 请求的&nbsp;<code>Cookie</code>&nbsp;头中是否存在名为<code>JSESSIONID</code>&nbsp;的 cookie，然后用它的值（session ID）从服务端内存中找到关联的&nbsp;<code>HttpSession</code>。</p>
<p>你可以在&nbsp;<code>web.xml</code>&nbsp;中设置&nbsp;<code>session-timeout</code>&nbsp;，默认值为 30 分钟。超时到达之前&nbsp;<code>HttpSession</code>会一直存活。所以当客户端不再访问该 web 应用超过 30 分钟后，Servlet 容器就会回收这个 session。后续每个请求，即使指定 cookie 名称也不能再访问到相同的 session。Servlet 容器会创建一个新的&nbsp;<code>Cookie</code>。</p>
<p>另一方面，客户端上的 session cookie 有一个默认存活时间，该事件和该浏览器实例运行时间一样长。所以，当客户端关闭该浏览器实例（所有标签和窗口）后，这个 session 就会被客户端回收。新浏览器实例不再发送与该 session 关联的 cookie。一个新的&nbsp;<code>request.getSession()</code>&nbsp;将会返回新的&nbsp;<code>HttpSession</code>&nbsp;并设置一个拥有新&nbsp;<code>session</code>&nbsp;ID 的 cookie。</p>
<h3>概述</h3>
<ul>
<li><code>ServletContext</code>&nbsp;与 web 应用存活时间一样长。它被所有 session 中的所有请求共享。</li>
<li>只要客户端一直与相同浏览器实例的web应用交互并且没有超时，HttpSession就会存在。</li>
<li><code>HttpServletRequest</code>&nbsp;和&nbsp;<code>HttpServletResponse</code>&nbsp;的存活时间为客户端发送完成到完整的响应（web 页面）到达的这段时间。不会被其他地方共享。</li>
<li><code>所有 Servlet</code>、<code>Filter</code>&nbsp;和&nbsp;<code>Listener</code>&nbsp;对象在 web 应用运行时都是活跃的。它们被所有 session 中的请求共享。</li>
<li>你设置在&nbsp;<code>HttpServletRequest</code>、<code>HttpServletResponse</code>&nbsp;和&nbsp;<code>HttpSession</code>&nbsp;中的所有属性在问题中的对象存活时都会一直保持存活。</li>
</ul>
<h4>线程安全</h4>
<p>即便如此，你最关心的可能是线程安全。你现在应该学习到 Servlet 和 filter 被所有请求共享。那是 Java 的一个优点，使得多个不同线程（读取 HTTP 请求）可以使用同一个实例。否则为每个请求重新创建线程的开销实在过于昂贵。</p>
<p>但你应该也意识到永远不要将任何 request 或 session 域中的数据赋值给 servlet 或 filter 的实例变量。它将会被所有其他 session 中的所有请求共享。那是非线程安全的！下面的示例对这种情况进行了展示：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">public</span> <span style="color: #0000ff;">class</span> ExampleServlet <span style="color: #0000ff;">extends</span><span style="color: #000000;"> HttpServlet {
 
    </span><span style="color: #0000ff;">private</span><span style="color: #000000;"> Object thisIsNOTThreadSafe;
 
    </span><span style="color: #0000ff;">protected</span> <span style="color: #0000ff;">void</span> doGet(HttpServletRequest request, HttpServletResponse response) <span style="color: #0000ff;">throws</span><span style="color: #000000;"> ServletException, IOException {
        Object thisIsThreadSafe;
 
        thisIsNOTThreadSafe </span>= request.setParameter("foo"); <span style="color: #008000;">//</span><span style="color: #008000;"> BAD!! Shared among all requests!</span>
        thisIsThreadSafe = request.getParameter("foo"); <span style="color: #008000;">//</span><span style="color: #008000;"> OK, this is thread safe.</span>
<span style="color: #000000;">    }
}</span></pre>
</div>
<h4>请参考：</h4>
<ul>
<li><a class="external" href="http://stackoverflow.com/questions/2095397/what-is-the-difference-between-jsf-servlet-and-jsp" rel="nofollow" target="_blank">JSF、Servlet 和 JSP 之间有什么不同？</a></li>
<li><a class="external" href="http://stackoverflow.com/questions/1700390/best-option-for-session-management-in-java" rel="nofollow" target="_blank">Java 中管理 Session 的最佳选择</a></li>
<li><a class="external" href="http://stackoverflow.com/questions/2349633/doget-and-dopost-in-servlets" rel="nofollow" target="_blank">Servlet 中的 doGet 与 doPost</a></li>
<li><a class="external" href="http://stackoverflow.com/questions/8011138/servlet-seems-to-handle-multiple-concurrent-requests-synchronously/" rel="nofollow" target="_blank">Servlet 似乎会同步处理多并发请求</a></li>
</ul>
<p>&nbsp;</p>
<hr />
<p>&nbsp;</p>
<p>原文链接：<a class="external" href="http://stackoverflow.com/questions/3106452/how-do-servlets-work-instantiation-shared-variables-and-multithreading/3106909#3106909" rel="nofollow" target="_blank">stackoverflow</a></p>
<p>首发至：<a href="http://www.importnew.com/17025.html">http://www.importnew.com/17025.html</a>，并已同步至 <a href="https://github.com/nitta-honoka/StackOverflow-Quora-More-translate" target="_blank">Github</a>，欢迎 Star 关注。</p>
