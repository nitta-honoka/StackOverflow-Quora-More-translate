<p><span data-rel="content">数据包围着我们。虽然搜索引擎和其他应用都对基于文本方式表示的数据偏爱有加，但人们发现可视化是更容易理解的一种方式。今年初，SitePoint 发表了 Aurelio 的文章<a href="http://www.sitepoint.com/creating-beautiful-charts-chart-js/">《 Chart.js简介》</a>。在深入研究&nbsp;<a href="http://www.chartjs.org/">Chart.js</a>&nbsp;的功能后，本文将会讲解这篇简介的一些重点。</span></p>
<h2>入门</h2>
<p>Chart.js 是一个基于 HTML5 canvas 的响应式、灵活的、轻量化的图表库。库中提供了六种不同的图表类型，每种类型都带有一系列的自定义选项。如果这些还不够，你还可以创造自己的图表类型。</p>
<p>Chart.js 的六种图表类型代码一共只有 11 kb 大，并做了 gzip 压缩处理，另外该库是模块化的，你可以仅仅使用自己需要的图表类型，从而进一步节省了空间。下面是包含该库的 cdnjs 链接。</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script </span><span style="color: #ff0000;">src</span><span style="color: #0000ff;">="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/1.0.2/Chart.min.js"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<h2>可用的设置项</h2>
<p>从提示信息到动画效果（校稿者注：tool tip是指鼠标移动到某个元素上弹出的提示信息），Chart.js 允许你改变图表的几乎所有特征。在本节，我将会修改一些设置，以展示 Chart.js 是如何被创建出来的。我们将从下面的 HTML 代码开始：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">canvas </span><span style="color: #ff0000;">id</span><span style="color: #0000ff;">="canvas"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">canvas</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>对于首次展示，我会创建一个折线图。为了使图表有意义，这里会有几个需要设置的基本选项。折线图需要一个标签数组和数据集。标签会显示在 X 轴。我已经为折线图模拟了一些数据，这些数据被分开放到一个数组里面去，每个数据有自己的填充颜色、折线和点集。</p>
<p>在这个例子中，我将&nbsp;<code>fillColor</code>设置为透明。如果你不设置&nbsp;<code>fillColor</code>&nbsp;的值，将默认设置为黑色或者灰色。这同样适用于其他值。色彩使用 RGBA、RGB、hex 或 HSL 格式定义，与 CSS 是一样的。</p>
<div class="cnblogs_code">
<pre><span style="color: #008080;"> 1</span> <span style="color: #0000ff;">var</span> lineData =<span style="color: #000000;"> {
</span><span style="color: #008080;"> 2</span>   labels: ['Data 1', 'Data 2', 'Data 3', 'Data 4'<span style="color: #000000;">, 
</span><span style="color: #008080;"> 3</span>            'Data 5', 'Data 6', 'Data 7'<span style="color: #000000;">],
</span><span style="color: #008080;"> 4</span> <span style="color: #000000;">  datasets: [{
</span><span style="color: #008080;"> 5</span>     fillColor: 'rgba(0,0,0,0)'<span style="color: #000000;">,
</span><span style="color: #008080;"> 6</span>     strokeColor: 'rgba(220,180,0,1)'<span style="color: #000000;">,
</span><span style="color: #008080;"> 7</span>     pointColor: 'rgba(220,180,0,1)'<span style="color: #000000;">,
</span><span style="color: #008080;"> 8</span>     data: [20, 30, 80, 20, 40, 10, 60<span style="color: #000000;">]
</span><span style="color: #008080;"> 9</span> <span style="color: #000000;">  }, {
</span><span style="color: #008080;">10</span>     fillColor: 'rgba(0,0,0,0)'<span style="color: #000000;">,
</span><span style="color: #008080;">11</span>     strokeColor: 'rgba(151,187,205,1)'<span style="color: #000000;">,
</span><span style="color: #008080;">12</span>     pointColor: 'rgba(151,187,205,1)'<span style="color: #000000;">,
</span><span style="color: #008080;">13</span>     data: [60, 10, 40, 30, 80, 30, 20<span style="color: #000000;">]
</span><span style="color: #008080;">14</span> <span style="color: #000000;">  }]
</span><span style="color: #008080;">15</span> }</pre>
</div>
<h3>设置全局选项</h3>
<p>在代码中我已经设置了一些全局值。<code>animationSteps</code>&nbsp;决定了动画的持续时间。根据需要，你可以修改更多的选项，比如&nbsp;<code>scaleLineColor</code>&nbsp;和&nbsp;<code>scaleIntegersOnly</code>。我建议浏览<a href="http://www.chartjs.org/docs/">Chart.js 文档</a>查看库中提供的其他选项。</p>
<div class="cnblogs_code">
<pre><span style="color: #008080;"> 1</span> Chart.defaults.global =<span style="color: #000000;"> {
</span><span style="color: #008080;"> 2</span>   animationSteps : 50<span style="color: #000000;">,
</span><span style="color: #008080;"> 3</span>   tooltipYPadding : 16<span style="color: #000000;">,
</span><span style="color: #008080;"> 4</span>   tooltipCornerRadius : 0<span style="color: #000000;">,
</span><span style="color: #008080;"> 5</span>   tooltipTitleFontStyle : 'normal'<span style="color: #000000;">,
</span><span style="color: #008080;"> 6</span>   tooltipFillColor : 'rgba(0,160,0,0.8)'<span style="color: #000000;">,
</span><span style="color: #008080;"> 7</span>   animationEasing : 'easeOutBounce'<span style="color: #000000;">,
</span><span style="color: #008080;"> 8</span>   scaleLineColor : 'black'<span style="color: #000000;">,
</span><span style="color: #008080;"> 9</span>   scaleFontSize : 16
<span style="color: #008080;">10</span> }</pre>
</div>
<h3>设置专有的图表选项</h3>
<p>除了全局选项，还有一些针对特定图表类型的配置选项。在这个折线图中，我将会设置这类选项，希望对你有所启发：</p>
<div class="cnblogs_code">
<pre><span style="color: #008080;">1</span> <span style="color: #0000ff;">var</span> ctx = document.getElementById('canvas').getContext('2d'<span style="color: #000000;">);
</span><span style="color: #008080;">2</span> <span style="color: #0000ff;">var</span> lineDemo = <span style="color: #0000ff;">new</span><span style="color: #000000;"> Chart(ctx).Line(lineData, {
</span><span style="color: #008080;">3</span>   responsive: <span style="color: #0000ff;">true</span><span style="color: #000000;">,
</span><span style="color: #008080;">4</span>   pointDotRadius: 10<span style="color: #000000;">,
</span><span style="color: #008080;">5</span>   bezierCurve: <span style="color: #0000ff;">false</span><span style="color: #000000;">,
</span><span style="color: #008080;">6</span>   scaleShowVerticalLines: <span style="color: #0000ff;">false</span><span style="color: #000000;">,
</span><span style="color: #008080;">7</span>   scaleGridLineColor: 'black'
<span style="color: #008080;">8</span> });</pre>
</div>
<p>Chart.js 生成的图表默认为非响应式。将&nbsp;<code>responsive</code>&nbsp;设置为 true 可以使其转化为响应式图表。如果你需要让每个图表都成为响应式的，我推荐设置全局值，就像这样：</p>
<div class="cnblogs_code">
<pre>Chart.defaults.global.responsive = <span style="color: #0000ff;">true</span>;</pre>
</div>
<p>&nbsp;</p>
<p>下面你会看见这个折线图的示例：</p>
<p class="codepen">See the Pen&nbsp;<a href="http://codepen.io/SitePoint/pen/mJRrKw/">Chart.js Responsive Line Chart Demo</a>&nbsp;by SitePoint (<a href="http://codepen.io/SitePoint">@SitePoint</a>) on&nbsp;<a href="http://codepen.io/">CodePen</a>.</p>
<h2>增加与移除动态数据</h2>
<p>有时你需要展示时刻变化的数据。股票市场便是这个应用场景的典型例子。这本节中我将会创建一个柱形图，并且在动态删除数据的同时增加数据。我会使用一些随机数据，并在这个例子中通过柱形图来展示数据。本例中的大部分代码与上一个例子相似。一旦我们拥有自己的 HTML（与上一个例子一样），便可以添加自己的 JavaScript。</p>
<p>首先我们需要编写代码将动态数据填充进图表。我使用function表达式生成随机值，然后将其赋给一个变量&nbsp;<code>dData</code>。这些值会在需要变化时为我们提供随机的数据。像之前的例子一样，我创建了一个标签数组和数据集，并设置了一个任意的&nbsp;<code>fillColor</code>。</p>
<div class="cnblogs_code">
<pre><span style="color: #008080;"> 1</span> <span style="color: #0000ff;">var</span> dData = <span style="color: #0000ff;">function</span><span style="color: #000000;">() {
</span><span style="color: #008080;"> 2</span>   <span style="color: #0000ff;">return</span> Math.round(Math.random() * 90) + 10<span style="color: #000000;">;
</span><span style="color: #008080;"> 3</span> <span style="color: #000000;">};
</span><span style="color: #008080;"> 4</span> 
<span style="color: #008080;"> 5</span> <span style="color: #0000ff;">var</span> barData =<span style="color: #000000;"> {
</span><span style="color: #008080;"> 6</span>   labels: ['dD 1', 'dD 2', 'dD 3', 'dD 4'<span style="color: #000000;">,
</span><span style="color: #008080;"> 7</span>            'dD 5', 'dD 6', 'dD 7', 'dD 8'<span style="color: #000000;">],
</span><span style="color: #008080;"> 8</span> <span style="color: #000000;">  datasets: [{
</span><span style="color: #008080;"> 9</span>     fillColor: 'rgba(0,60,100,1)'<span style="color: #000000;">,
</span><span style="color: #008080;">10</span>     strokeColor: 'black'<span style="color: #000000;">,
</span><span style="color: #008080;">11</span> <span style="color: #000000;">    data: [dData(), dData(), dData(), dData(),
</span><span style="color: #008080;">12</span> <span style="color: #000000;">           dData(), dData(), dData(), dData()]
</span><span style="color: #008080;">13</span> <span style="color: #000000;">  }]
</span><span style="color: #008080;">14</span> }</pre>
</div>
<p>&nbsp;</p>
<p>现在是时候编写代码来为我们的图表删除与添加柱形了。开始时我们初始化&nbsp;<code>index</code>&nbsp;的值为 11，我使用了两个方法：<code>removeData()</code>&nbsp;和&nbsp;<code>addData(valuesArray,label)</code>。调用实例的&nbsp;<code>removeData()</code>&nbsp;方法删除图表所有数据集的第一个值。在&nbsp;<code>barChartDemo</code>&nbsp;这个例子中，数据集的第一个值被移除了。调用&nbsp;<code>addData()</code>&nbsp;顺着标签传递一个数组值，在图表的最后增加一个新的数据节点。下面的代码片段每 3 秒钟会更新一次图表。</p>
<div class="cnblogs_code">
<pre><span style="color: #008080;"> 1</span> <span style="color: #0000ff;">var</span> index = 11<span style="color: #000000;">;
</span><span style="color: #008080;"> 2</span> <span style="color: #0000ff;">var</span> ctx = document.getElementById('canvas').getContext('2d'<span style="color: #000000;">);
</span><span style="color: #008080;"> 3</span> <span style="color: #0000ff;">var</span> barDemo = <span style="color: #0000ff;">new</span><span style="color: #000000;"> Chart(ctx).Bar(barData, {
</span><span style="color: #008080;"> 4</span>   responsive: <span style="color: #0000ff;">true</span>
<span style="color: #008080;"> 5</span> <span style="color: #000000;">});
</span><span style="color: #008080;"> 6</span> 
<span style="color: #008080;"> 7</span> setInterval(<span style="color: #0000ff;">function</span><span style="color: #000000;">() {
</span><span style="color: #008080;"> 8</span> <span style="color: #000000;">  barDemo.removeData();
</span><span style="color: #008080;"> 9</span>   barDemo.addData([dData()], 'dD ' +<span style="color: #000000;"> index);
</span><span style="color: #008080;">10</span>   index++<span style="color: #000000;">;
</span><span style="color: #008080;">11</span> }, 3000);</pre>
</div>
<p>&nbsp;</p>
<p>另一个更新图表数值的方法是直接设置数值。在下面的例子中，第一行是将第一个数据集的第二个柱形的数值设为 60。如果你在这时更新，柱形会通过动画将其当前值变为 60。</p>
<div class="cnblogs_code">
<pre>barDemo.datasets[0].bars[2].value = 60<span style="color: #000000;">;
barDemo.update();</span></pre>
</div>
<p>&nbsp;</p>
<p>这里是柱形图的示例（由SitePoint在CodePen上创建）：</p>
<p>See the Pen&nbsp;<a href="http://codepen.io/SitePoint/pen/Kpager/">Chart.js Responsive Bar Chart Demo</a>&nbsp;by SitePoint (<a href="http://codepen.io/SitePoint">@SitePoint</a>) on&nbsp;<a href="http://codepen.io/">CodePen</a>.</p>
<h2>结论</h2>
<p>这个教程覆盖了关于 Chart.js 的一些重要功能。第一个例子展示了一些全局设置的使用，同时，Chart.js也为每个图表类型提供了专属的自定义设置。如果当前可用的图表无法满足你的需求，你还可以创造自己的图表类型。我推荐你浏览<a href="http://www.chartjs.org/">文档</a>，加深关于该库什么可以做，什么无法做的认识。</p>
<hr />
<p>本文首发至&nbsp;<a href="http://web.jobbole.com/83760/" target="_blank">伯乐在线</a>&nbsp;- 感谢&nbsp;<a href="http://www.jobbole.com/members/mybreeze77">Justin Wu</a>&nbsp;校稿。<br />英文出处：<a href="http://www.sitepoint.com/fancy-responsive-charts-with-chart-js" target="_blank">Monty Shokeen</a>。</p>
<p>已同步至 <a href="https://github.com/nitta-honoka/StackOverflow-Quora-More-translate" target="_blank">Github</a>，欢迎 Star 关注更新。</p>