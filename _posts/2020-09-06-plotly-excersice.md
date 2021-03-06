---
layout: post
title: "[시각화] plotly 라이브러리로 깃허브 블로그에 반응형 그래프 넣기 "
subtitle: "Labelling Lines with Annotations 예시"
date: 2020-09-05 11:11:13 -0400
background: '/img/posts/01.jpg'
datatable: true
comments: true
category : Data Science
---

<html>
<head>
  <!-- Plotly.js -->
  <script src="https://cdn.plot.ly/plotly-1.2.0.min.js"></script>

  <!-- highlight.js-->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/9.13.1/styles/vs2015.min.css">
  <script src="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/9.13.1/highlight.min.js"></script>
  <script>hljs.initHighlightingOnLoad();</script>
</head>

<body>
<h1>
  목표<br/>
</h1>

<p>
    javascript 시각화 오픈소스 중 하나인 plotly를 이용해서, 반응형 그래프를 넣어보자
</p>

<h3>
  1. plotly.js CDN 임포트<br/>
</h3>
<p>
    - header 에 아래 코드를 입력하여, CDN을 가져온다.<br/>
    - plotly-1.2.0 와 같이 특정버전을 지정할 수도 있고, plotly-latest로 하면 최신버전을 가져오게 할수도 있다.<br/><br/>
</p>
<pre><code class="html">
  &lt;header&gt;
    &lt;script&gt;script src="https://cdn.plot.ly/plotly-1.2.0.min.js">&lt;/script&gt;
  &lt;/header&gt;

</code></pre>
<br/><br/>

<h3>
  2. 그래프가 들어갈 div 생성<br/>
</h3>
<p>
    - 그래프의 사이즈에 맞게, width와 height값을 조정<br/><br/>
</p>
<pre><code class="html">
  &lt;div id="tester" style="width:100%;height:800px;"&gt;&lt;/div&gt;

</code></pre>
<br/><br/>

<h3>
  3. div에 들어갈 그래프 넣기<br/>
</h3>
<p>
  - <a href="https://plotly.com/javascript/line-charts/#labelling-lines-with-annotations">labelling-lines-with-annotations</a>의 샘플 코드를 활용<br/><br/>
</p>
<pre><code class="html">
  &lt;script&gt;
    var xData = [
      [2001, 2002, 2003, 2004, 2005, 2006, 2007, 2008, 2009, 2010, 2011, 2013],
      [2001, 2002, 2003, 2004, 2005, 2006, 2007, 2008, 2009, 2010, 2011, 2013],
      [2001, 2002, 2003, 2004, 2005, 2006, 2007, 2008, 2009, 2010, 2011, 2013],
      [2001, 2002, 2003, 2004, 2005, 2006, 2007, 2008, 2009, 2010, 2011, 2013]
    ];

    var yData = [
      [74, 82, 80, 74, 73, 72, 74, 70, 70, 66, 66, 69],
      [45, 42, 50, 46, 36, 36, 34, 35, 32, 31, 31, 28],
      [13, 14, 20, 24, 20, 24, 24, 40, 35, 41, 43, 50],
      [18, 21, 18, 21, 16, 14, 13, 18, 17, 16, 19, 23]
    ];

    var colors = ['rgba(67,67,67,1)', 'rgba(115,115,115,1)', 'rgba(49,130,189, 1)',
      'rgba(189,189,189,1)'
    ];

    var lineSize = [2, 2, 4, 2];

    var labels = ['Television', 'Newspaper', 'Internet', 'Radio'];

    var data = [];

    for ( var i = 0 ; i < xData.length ; i++ ) {
      var result = {
        x: xData[i],
        y: yData[i],
        type: 'scatter',
        mode: 'lines',
        line: {
          color: colors[i],
          width: lineSize[i]
        }
      };
      var result2 = {
        x: [xData[i][0], xData[i][11]],
        y: [yData[i][0], yData[i][11]],
        type: 'scatter',
        mode: 'markers',
        marker: {
          color: colors[i],
          size: 12
        }
      };
      data.push(result, result2);
    }

    var layout = {
      showlegend: false,
      height: 600,
      width: 600,
      xaxis: {
        showline: true,
        showgrid: false,
        showticklabels: true,
        linecolor: 'rgb(204,204,204)',
        linewidth: 2,
        autotick: false,
        ticks: 'outside',
        tickcolor: 'rgb(204,204,204)',
        tickwidth: 2,
        ticklen: 5,
        tickfont: {
          family: 'Arial',
          size: 12,
          color: 'rgb(82, 82, 82)'
        }
      },
      yaxis: {
        showgrid: false,
        zeroline: false,
        showline: false,
        showticklabels: false
      },
      autosize: false,
      margin: {
        autoexpand: false,
        l: 100,
        r: 20,
        t: 100
      },
      annotations: [
        {
          xref: 'paper',
          yref: 'paper',
          x: 0.0,
          y: 1.05,
          xanchor: 'left',
          yanchor: 'bottom',
          text: 'Main Source for News',
          font:{
            family: 'Arial',
            size: 30,
            color: 'rgb(37,37,37)'
          },
          showarrow: false
        },
        {
          xref: 'paper',
          yref: 'paper',
          x: 0.5,
          y: -0.1,
          xanchor: 'center',
          yanchor: 'top',
          text: 'Source: Pew Research Center & Storytelling with data',
          showarrow: false,
          font: {
            family: 'Arial',
            size: 12,
            color: 'rgb(150,150,150)'
          }
        }
      ]
    };

    for( var i = 0 ; i < xData.length ; i++ ) {
      var result = {
        xref: 'paper',
        x: 0.05,
        y: yData[i][0],
        xanchor: 'right',
        yanchor: 'middle',
        text: labels[i] + ' ' + yData[i][0] +'%',
        showarrow: false,
        font: {
          family: 'Arial',
          size: 16,
          color: 'black'
        }
      };
      var result2 = {
        xref: 'paper',
        x: 0.95,
        y: yData[i][11],
        xanchor: 'left',
        yanchor: 'middle',
        text: yData[i][11] +'%',
        font: {
          family: 'Arial',
          size: 16,
          color: 'black'
        },
        showarrow: false
      };

      layout.annotations.push(result, result2);
    }
    
    Plotly.newPlot('tester', data, layout);
  &lt;/script&gt;
</code></pre>
<br/>

<p>
  그러고나면, 아래와 같은 반응형 그래프가 그려지는 것을 확인할 수 있다.<br/><br/>
</p>

<div id="tester" style="width:100%;height:600px;"></div>

<script>
  var xData = [
    [2001, 2002, 2003, 2004, 2005, 2006, 2007, 2008, 2009, 2010, 2011, 2013],
    [2001, 2002, 2003, 2004, 2005, 2006, 2007, 2008, 2009, 2010, 2011, 2013],
    [2001, 2002, 2003, 2004, 2005, 2006, 2007, 2008, 2009, 2010, 2011, 2013],
    [2001, 2002, 2003, 2004, 2005, 2006, 2007, 2008, 2009, 2010, 2011, 2013]
  ];

  var yData = [
    [74, 82, 80, 74, 73, 72, 74, 70, 70, 66, 66, 69],
    [45, 42, 50, 46, 36, 36, 34, 35, 32, 31, 31, 28],
    [13, 14, 20, 24, 20, 24, 24, 40, 35, 41, 43, 50],
    [18, 21, 18, 21, 16, 14, 13, 18, 17, 16, 19, 23]
  ];

  var colors = ['rgba(67,67,67,1)', 'rgba(115,115,115,1)', 'rgba(49,130,189, 1)',
    'rgba(189,189,189,1)'
  ];

  var lineSize = [2, 2, 4, 2];

  var labels = ['Television', 'Newspaper', 'Internet', 'Radio'];

  var data = [];

  for ( var i = 0 ; i < xData.length ; i++ ) {
    var result = {
      x: xData[i],
      y: yData[i],
      type: 'scatter',
      mode: 'lines',
      line: {
        color: colors[i],
        width: lineSize[i]
      }
    };
    var result2 = {
      x: [xData[i][0], xData[i][11]],
      y: [yData[i][0], yData[i][11]],
      type: 'scatter',
      mode: 'markers',
      marker: {
        color: colors[i],
        size: 12
      }
    };
    data.push(result, result2);
  }

  var layout = {
    showlegend: false,
    height: 600,
    width: 600,
    xaxis: {
      showline: true,
      showgrid: false,
      showticklabels: true,
      linecolor: 'rgb(204,204,204)',
      linewidth: 2,
      autotick: false,
      ticks: 'outside',
      tickcolor: 'rgb(204,204,204)',
      tickwidth: 2,
      ticklen: 5,
      tickfont: {
        family: 'Arial',
        size: 12,
        color: 'rgb(82, 82, 82)'
      }
    },
    yaxis: {
      showgrid: false,
      zeroline: false,
      showline: false,
      showticklabels: false
    },
    autosize: false,
    margin: {
      autoexpand: false,
      l: 100,
      r: 20,
      t: 100
    },
    annotations: [
      {
        xref: 'paper',
        yref: 'paper',
        x: 0.0,
        y: 1.05,
        xanchor: 'left',
        yanchor: 'bottom',
        text: 'Main Source for News',
        font:{
          family: 'Arial',
          size: 30,
          color: 'rgb(37,37,37)'
        },
        showarrow: false
      },
      {
        xref: 'paper',
        yref: 'paper',
        x: 0.5,
        y: -0.1,
        xanchor: 'center',
        yanchor: 'top',
        text: 'Source: Pew Research Center & Storytelling with data',
        showarrow: false,
        font: {
          family: 'Arial',
          size: 12,
          color: 'rgb(150,150,150)'
        }
      }
    ]
  };

  for( var i = 0 ; i < xData.length ; i++ ) {
    var result = {
      xref: 'paper',
      x: 0.05,
      y: yData[i][0],
      xanchor: 'right',
      yanchor: 'middle',
      text: labels[i] + ' ' + yData[i][0] +'%',
      showarrow: false,
      font: {
        family: 'Arial',
        size: 16,
        color: 'black'
      }
    };
    var result2 = {
      xref: 'paper',
      x: 0.95,
      y: yData[i][11],
      xanchor: 'left',
      yanchor: 'middle',
      text: yData[i][11] +'%',
      font: {
        family: 'Arial',
        size: 16,
        color: 'black'
      },
      showarrow: false
    };

    layout.annotations.push(result, result2);
  }
  
  Plotly.newPlot('tester', data, layout);
</script>
<br/><br/>

<h3>
  참고자료<br/>
</h3>
<p>
  - <a href="https://bit.ly/1Or9igj">plotly.js 공식문서</a><br/>
  - <a href="https://plotly.com/javascript/getting-started">plotly.js 시작하기</a><br/>
</p>
<br/><br/>

</body>
</html>



{% if page.comments %} 

<div id="disqus_thread"></div>
<script>

/**
*  RECOMMENDED CONFIGURATION VARIABLES: EDIT AND UNCOMMENT THE SECTION BELOW TO INSERT DYNAMIC VALUES FROM YOUR PLATFORM OR CMS.
*  LEARN WHY DEFINING THESE VARIABLES IS IMPORTANT: https://disqus.com/admin/universalcode/#configuration-variables*/
/*
var disqus_config = function () {
this.page.url = PAGE_URL;  // Replace PAGE_URL with your page's canonical URL variable
this.page.identifier = PAGE_IDENTIFIER; // Replace PAGE_IDENTIFIER with your page's unique identifier variable
};
*/
(function() { // DON'T EDIT BELOW THIS LINE
var d = document, s = d.createElement('script');
s.src = 'https://jirehbak.disqus.com/embed.js';
s.setAttribute('data-timestamp', +new Date());
(d.head || d.body).appendChild(s);
})();
</script>
<noscript>Please enable JavaScript to view the <a href="https://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
                            
{% endif %}