<h3><span data-rel="content"><span style="font-size: 1.17em; line-height: 1.5;">回到顶部按钮</span></span></h3>
<p>通过使用 jQuery 中的&nbsp;<code>animate</code>&nbsp;和&nbsp;<code>scrollTop</code>&nbsp;方法，你无需插件便可创建一个简单地回到顶部动画：</p>
<div class="cnblogs_code">
<pre><span style="color: #008080;">1</span> <span style="color: #008000;">//</span><span style="color: #008000;"> Back to top</span>
<span style="color: #008080;">2</span> $('a.top').click(<span style="color: #0000ff;">function</span><span style="color: #000000;"> (e) {
</span><span style="color: #008080;">3</span> <span style="color: #000000;">  e.preventDefault();
</span><span style="color: #008080;">4</span>   $(document.body).animate({scrollTop: 0}, 800<span style="color: #000000;">);
</span><span style="color: #008080;">5</span> });</pre>
</div>
<div class="cnblogs_code">
<pre><span style="color: #008080;">1</span> &lt;!-- Create an anchor tag --&gt;
<span style="color: #008080;">2</span> &lt;a class="top" href="#"&gt;Back to top&lt;/a&gt;</pre>
</div>
<p>将&nbsp;<code>scrollTop</code>&nbsp;的值改为你想要 scrollbar 停止的地方。然后你要做的就是，设置在 800 毫秒内回到顶部。</p>
<h3>预加载图片</h3>
<p>如果你的页面使用了大量不能初始可见的图片（例如绑定在 hover 上），预加载它们是十分有用的：</p>
<div class="cnblogs_code">
<pre><span style="color: #008080;">1</span> $.preloadImages = <span style="color: #0000ff;">function</span><span style="color: #000000;"> () {
</span><span style="color: #008080;">2</span>   <span style="color: #0000ff;">for</span> (<span style="color: #0000ff;">var</span> i = 0; i &lt; arguments.length; i++<span style="color: #000000;">) {
</span><span style="color: #008080;">3</span>     $('&lt;img&gt;').attr('src'<span style="color: #000000;">, arguments[i]);
</span><span style="color: #008080;">4</span> <span style="color: #000000;">  }
</span><span style="color: #008080;">5</span> <span style="color: #000000;">};
</span><span style="color: #008080;">6</span>  
<span style="color: #008080;">7</span> $.preloadImages('img/hover-on.png', 'img/hover-off.png');</pre>
</div>
<h3>检查图片是否加载完毕</h3>
<p>有时你或许要检查图片是否完全加载完毕，才能在脚本中进行后续操作：</p>
<div class="cnblogs_code">
<pre><span style="color: #008080;">1</span> $('img').load(<span style="color: #0000ff;">function</span><span style="color: #000000;"> () {
</span><span style="color: #008080;">2</span>   console.log('image load successful'<span style="color: #000000;">);
</span><span style="color: #008080;">3</span> });</pre>
</div>
<p>你也可以通过把 img 标签替换成 ID 或 class，来检查特定图片是否加载完成。</p>
<h3>自动修复损坏的图片</h3>
<p>如果你发现自己网站的图片链接挂了，一个一个替换很麻烦。这段简单的代码可以帮上大忙：</p>
<div class="cnblogs_code">
<pre><span style="color: #008080;">1</span> $('img').on('error', <span style="color: #0000ff;">function</span><span style="color: #000000;"> () {
</span><span style="color: #008080;">2</span>   $(<span style="color: #0000ff;">this</span>).prop('src', 'img/broken.png'<span style="color: #000000;">);
</span><span style="color: #008080;">3</span> });</pre>
</div>
<p>即使你没有任何损坏的链接，增加这段代码也不会有什么影响。</p>
<h3>Hover 上的 Class 切换</h3>
<p>如果用户的鼠标悬停在页面上某个可点击元素时，你想要改变这个元素的视觉表现。可以使用下面这段代码，当用户悬停时，为该元素增加一个 class；当用户鼠标离开后移除这个 class：</p>
<div class="cnblogs_code">
<pre><span style="color: #008080;">1</span> $('.btn').hover(<span style="color: #0000ff;">function</span><span style="color: #000000;"> () {
</span><span style="color: #008080;">2</span>   $(<span style="color: #0000ff;">this</span>).addClass('hover'<span style="color: #000000;">);
</span><span style="color: #008080;">3</span> }, <span style="color: #0000ff;">function</span><span style="color: #000000;"> () {
</span><span style="color: #008080;">4</span>   $(<span style="color: #0000ff;">this</span>).removeClass('hover'<span style="color: #000000;">);
</span><span style="color: #008080;">5</span> });</pre>
</div>
<p>你仅需增加必须的 CSS。如果需要更简单的方式，还可以使用&nbsp;<code>toggleClass</code>&nbsp;方法：</p>
<div class="cnblogs_code">
<pre><span style="color: #008080;">1</span> $('.btn').hover(<span style="color: #0000ff;">function</span><span style="color: #000000;"> () {
</span><span style="color: #008080;">2</span>   $(<span style="color: #0000ff;">this</span>).toggleClass('hover'<span style="color: #000000;">);
</span><span style="color: #008080;">3</span> });</pre>
</div>
<p><strong>注意</strong>：CSS 或许是这个例子更快速的解决方式，但大家仍然值得知道这一点。</p>
<h3>禁用 input 字段</h3>
<p>有时你也许想让表单的提交按钮或其文本输入框变得不可用，直到用户执行了一个特定行为（例如确认 &ldquo;我已经阅读该条款&rdquo; 的复选框）。增加&nbsp;<code>disabled</code>&nbsp;attribute 到你的 input，就可以实现自己想要的效果：</p>
<div class="cnblogs_code">
<pre><span style="color: #008080;">1</span> $('input[type="submit"]').prop('disabled', <span style="color: #0000ff;">true</span>);</pre>
</div>
<p>当你想把&nbsp;<code>disabled</code>&nbsp;的值改为&nbsp;<code>false</code>&nbsp;时，仅需在该 input 上再运行一次&nbsp;<code>prop</code>&nbsp;方法。</p>
<div class="cnblogs_code">
<pre><span style="color: #008080;">1</span> $('input[type="submit"]').prop('disabled', <span style="color: #0000ff;">false</span>);</pre>
</div>
<h3>停止链接加载</h3>
<p>有时你不想链接跳转到某个页面或重加载该页面，而希望可以做一些其他事情，比如触发其他脚本。下面的代码是禁止默认行为的一个小诀窍：</p>
<div class="cnblogs_code">
<pre><span style="color: #008080;">1</span> $('a.no-link').click(<span style="color: #0000ff;">function</span><span style="color: #000000;"> (e) {
</span><span style="color: #008080;">2</span> <span style="color: #000000;">  e.preventDefault();
</span><span style="color: #008080;">3</span> });</pre>
</div>
<h3>淡入淡出/滑动开关</h3>
<p>淡入淡出与滑动是我们经常使用 jQuery&nbsp;做成的动画效果。或许你只是想在用户点击某物时展现一个元素，使用&nbsp;<code>fadeIn</code>&nbsp;和&nbsp;<code>slideDown</code>&nbsp;都很棒。但如果想让该元素在第一次点击时显现，第二次点击时消失，下面的代码可以很好地完成这个工作：</p>
<div id="crayon-5647e570e20d6708820062" class="crayon-syntax crayon-theme-github crayon-font-monaco crayon-os-mac print-yes notranslate" data-settings=" minimize scroll-always">
<div class="crayon-toolbar" data-settings=" show">
<div class="crayon-tools">
<div class="crayon-button crayon-nums-button crayon-pressed" title="切换是否显示行编号">
<div class="cnblogs_code">
<pre><span style="color: #008080;">1</span> <span style="color: #008000;">//</span><span style="color: #008000;"> Fade</span>
<span style="color: #008080;">2</span> $('.btn').click(<span style="color: #0000ff;">function</span><span style="color: #000000;"> () {
</span><span style="color: #008080;">3</span>   $('.element').fadeToggle('slow'<span style="color: #000000;">);
</span><span style="color: #008080;">4</span> <span style="color: #000000;">});
</span><span style="color: #008080;">5</span>  
<span style="color: #008080;">6</span> <span style="color: #008000;">//</span><span style="color: #008000;"> Toggle</span>
<span style="color: #008080;">7</span> $('.btn').click(<span style="color: #0000ff;">function</span><span style="color: #000000;"> () {
</span><span style="color: #008080;">8</span>   $('.element').slideToggle('slow'<span style="color: #000000;">);
</span><span style="color: #008080;">9</span> });</pre>
</div>
</div>
</div>
</div>
</div>
<h3>简单的手风琴效果</h3>
<p>这是一个快速实现手风琴效果的简单方法：</p>
<div class="cnblogs_code">
<pre><span style="color: #008080;"> 1</span> <span style="color: #008000;">//</span><span style="color: #008000;"> Close all panels</span>
<span style="color: #008080;"> 2</span> $('#accordion').find('.content'<span style="color: #000000;">).hide();
</span><span style="color: #008080;"> 3</span>  
<span style="color: #008080;"> 4</span> <span style="color: #008000;">//</span><span style="color: #008000;"> Accordion</span>
<span style="color: #008080;"> 5</span> $('#accordion').find('.accordion-header').click(<span style="color: #0000ff;">function</span><span style="color: #000000;"> () {
</span><span style="color: #008080;"> 6</span>   <span style="color: #0000ff;">var</span> next = $(<span style="color: #0000ff;">this</span><span style="color: #000000;">).next();
</span><span style="color: #008080;"> 7</span>   next.slideToggle('fast'<span style="color: #000000;">);
</span><span style="color: #008080;"> 8</span>   $('.content').not(next).slideUp('fast'<span style="color: #000000;">);
</span><span style="color: #008080;"> 9</span>   <span style="color: #0000ff;">return</span> <span style="color: #0000ff;">false</span><span style="color: #000000;">;
</span><span style="color: #008080;">10</span> });</pre>
</div>
<p>增加这段脚本后，你所需做的所有事就是，查看脚本是否在必须的 HTML 中正常工作。</p>
<h3>使两个 Div 高度一样</h3>
<p>有时你也许想让两个 div 拥有同样高度，不管它们里面有什么内容：</p>
<div class="cnblogs_code">
<pre><span style="color: #008080;">1</span> ('.div').css('min-height', $('.main-div').height());</pre>
</div>
<p>该例设置了&nbsp;<code>min-height</code>，意味着它可以比主要 div 更大，但永远不能更小。但有一个更加灵活的方法是遍历一组元素的设置，然后将高度设为元素中的最高值：</p>
<div class="cnblogs_code">
<pre><span style="color: #008080;">1</span> <span style="color: #0000ff;">var</span> $columns = $('.column'<span style="color: #000000;">);
</span><span style="color: #008080;">2</span> <span style="color: #0000ff;">var</span> height = 0<span style="color: #000000;">;
</span><span style="color: #008080;">3</span> $columns.each(<span style="color: #0000ff;">function</span><span style="color: #000000;"> () {
</span><span style="color: #008080;">4</span>   <span style="color: #0000ff;">if</span> ($(<span style="color: #0000ff;">this</span>).height() &amp;<span style="color: #000000;">gt; height) {
</span><span style="color: #008080;">5</span>     height = $(<span style="color: #0000ff;">this</span><span style="color: #000000;">).height();
</span><span style="color: #008080;">6</span> <span style="color: #000000;">  }
</span><span style="color: #008080;">7</span> <span style="color: #000000;">});
</span><span style="color: #008080;">8</span> $columns.height(height);</pre>
</div>
<p>如果你想让所有列都有相同高度：</p>
<div class="cnblogs_code">
<pre><span style="color: #008080;">1</span> <span style="color: #0000ff;">var</span> $rows = $('.same-height-columns'<span style="color: #000000;">);
</span><span style="color: #008080;">2</span> $rows.each(<span style="color: #0000ff;">function</span><span style="color: #000000;"> () {
</span><span style="color: #008080;">3</span>   $(<span style="color: #0000ff;">this</span>).find('.column').height($(<span style="color: #0000ff;">this</span><span style="color: #000000;">).height());
</span><span style="color: #008080;">4</span> });&nbsp;</pre>
</div>
<h3>在新标签/窗口打开站外链接</h3>
<p>在一个新标签或者新窗口中打开外置链接，并确保站内链接会在相同的标签或窗口中打开：</p>
<div class="cnblogs_code">
<pre><span style="color: #008080;">1</span> $('a[href^="http"]').attr('target', '_blank'<span style="color: #000000;">);
</span><span style="color: #008080;">2</span> $('a[href^="//"]').attr('target', '_blank'<span style="color: #000000;">);
</span><span style="color: #008080;">3</span> $('a[href^="' + window.location.origin + '"]').attr('target', '_self');</pre>
</div>
<p><strong>注意</strong>：<code>window.location.origin</code>&nbsp;在 IE 10 中不可用，该 issue 的<a href="http://tosbourn.com/a-fix-for-window-location-origin-in-internet-explorer/">修复方法</a>。</p>
<h3>通过文本找到元素</h3>
<p>通过使用 jQuery 中的&nbsp;<code>contains()</code>&nbsp;选择器，你可以找到某个元素中的文本。如果文本不存在，该元素将会隐藏：</p>
<div class="cnblogs_code">
<pre><span style="color: #008080;">1</span> <span style="color: #0000ff;">var</span> search = $('#search'<span style="color: #000000;">).val();
</span><span style="color: #008080;">2</span> $('div:not(:contains("' + search + '"))').hide();</pre>
</div>
<h3>视觉改变触发</h3>
<p>当用户焦点在另外一个标签上，或重新回到标签时，触发 JavaScript：</p>
<div class="cnblogs_code">
<pre><span style="color: #008080;">1</span> $(document).on('visibilitychange', <span style="color: #0000ff;">function</span><span style="color: #000000;"> (e) {
</span><span style="color: #008080;">2</span>   <span style="color: #0000ff;">if</span> (e.target.visibilityState === "visible"<span style="color: #000000;">) {
</span><span style="color: #008080;">3</span>     console.log('Tab is now in view!'<span style="color: #000000;">);
</span><span style="color: #008080;">4</span>   } <span style="color: #0000ff;">else</span> <span style="color: #0000ff;">if</span> (e.target.visibilityState === "hidden"<span style="color: #000000;">) {
</span><span style="color: #008080;">5</span>     console.log('Tab is now hidden!'<span style="color: #000000;">);
</span><span style="color: #008080;">6</span> <span style="color: #000000;">  }
</span><span style="color: #008080;">7</span> });</pre>
</div>
<h3>Ajax 调用的错误处理</h3>
<p>当某次 Ajax 调用返回 404 或 500 错误，就会执行错误处理。但如果没有定义该处理，其他 jQuery 代码或许会停止工作。可以通过下面这段代码定义一个全局 Ajax 错误处理：</p>
<div class="cnblogs_code">
<pre><span style="color: #008080;">1</span> $(document).ajaxError(<span style="color: #0000ff;">function</span><span style="color: #000000;"> (e, xhr, settings, error) {
</span><span style="color: #008080;">2</span> <span style="color: #000000;">  console.log(error);
</span><span style="color: #008080;">3</span> });</pre>
</div>
<h3>插件链式调用</h3>
<p>jQuery 支持链式调用插件，以减缓反复查询 DOM，并创建多个 jQuery 对象。看下面示例代码：</p>
<div class="cnblogs_code">
<pre><span style="color: #008080;">1</span> $('#elem'<span style="color: #000000;">).show();
</span><span style="color: #008080;">2</span> $('#elem').html('bla'<span style="color: #000000;">);
</span><span style="color: #008080;">3</span> $('#elem').otherStuff();</pre>
</div>
<p>上面这段代码，可以通过链式操作大大改进：</p>
<div class="cnblogs_code">
<pre><span style="color: #008080;">1</span> $('#elem'<span style="color: #000000;">)
</span><span style="color: #008080;">2</span> <span style="color: #000000;">  .show()
</span><span style="color: #008080;">3</span>   .html('bla'<span style="color: #000000;">)
</span><span style="color: #008080;">4</span>   .otherStuff();</pre>
</div>
<p>还有另外一种方法，把元素缓存在变量中（前缀是 &nbsp;<code>$&nbsp;</code>）：</p>
<div class="cnblogs_code">
<pre><span style="color: #008080;">1</span> <span style="color: #0000ff;">var</span> $elem = $('#elem'<span style="color: #000000;">);
</span><span style="color: #008080;">2</span> <span style="color: #000000;">$elem.hide();
</span><span style="color: #008080;">3</span> $elem.html('bla'<span style="color: #000000;">);
</span><span style="color: #008080;">4</span> $elem.otherStuff();</pre>
</div>
<div id="crayon-5647e570e2113331594291" class="crayon-syntax crayon-theme-github crayon-font-monaco crayon-os-mac print-yes notranslate" data-settings=" minimize scroll-always">jQuery 中的链式操作和缓存方法，都极大精简和提速了代码。</div>
<div class="crayon-syntax crayon-theme-github crayon-font-monaco crayon-os-mac print-yes notranslate" data-settings=" minimize scroll-always"><hr />本文首发至&nbsp;<a href="http://web.jobbole.com/84028/" target="_blank">伯乐在线</a>，感谢&nbsp;<a href="http://www.jobbole.com/members/huanglimin">黄利民</a>&nbsp;校稿。<br />原文出处：<a href="https://github.com/AllThingsSmitty/jquery-tips-everyone-should-know" target="_blank">Matt Smith</a>。</div>