<!DOCTYPE html>
<html ⚡ lang="zh">
	<head>
		<script async custom-element="amp-auto-ads"
        src="https://cdn.ampproject.org/v0/amp-auto-ads-0.1.js">
		</script><meta charset="utf-8">
<meta name="viewport" content="width=device-width,minimum-scale=1,initial-scale=1">

<title>怎样在ipv6 only 的vps上安装v2ray&#43;ws&#43;TLS&#43;CDN？</title><meta name="description" content="本地网络没有ipv6但是有台免费的ipv6 only vps怎么使用啊，这里介绍使用cloudflare的cdn让你的本地可以使用这种ipv6 only vps的网络。" />
<link rel="canonical" href="https://huhu.blue/how-to-combine-cloudflare-with-ipv6-only-vps/" >
<link rel="sitemap" href="https://huhu.blue/sitemap.xml" type="application/xml" /><meta name="theme-color" content="#078aed"/>
<link rel="manifest" href="https://huhu.blue/manifest.json"><style amp-boilerplate>body{-webkit-animation:-amp-start 8s steps(1,end) 0s 1 normal both;-moz-animation:-amp-start 8s steps(1,end) 0s 1 normal both;-ms-animation:-amp-start 8s steps(1,end) 0s 1 normal both;animation:-amp-start 8s steps(1,end) 0s 1 normal both}@-webkit-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-moz-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-ms-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@-o-keyframes -amp-start{from{visibility:hidden}to{visibility:visible}}@keyframes  -amp-start{from{visibility:hidden}to{visibility:visible}}</style>
<noscript>
    <style amp-boilerplate>body{-webkit-animation:none;-moz-animation:none;-ms-animation:none;animation:none}</style>
</noscript><style amp-custom>
    
        *,*::before,*::after{box-sizing:border-box}ul[class],ol[class]{padding:0}body,h1,h2,h3,h4,p,ul[class],ol[class],li,figure,figcaption,blockquote,dl,dd{margin:0}body{min-height:100vh;scroll-behavior:smooth;text-rendering:optimizeSpeed}ul[class],ol[class]{list-style:none}a:not([class]){text-decoration-skip-ink:auto}img{max-width:100%;display:block}input,button,textarea,select{font:inherit}.chroma{background-color:#fff}.chroma .err{color:#a61717;background-color:#e3d2d2}.chroma .lntd{vertical-align:top;padding:0;margin:0;border:0}.chroma .lntable{border-spacing:0;padding:0;margin:0;border:0;width:auto;overflow:auto;display:block}.chroma .hl{display:block;width:100%;background-color:#ffc}.chroma .lnt{margin-right:.4em;padding:0 .4em;color:#7f7f7f}.chroma .ln{margin-right:.4em;padding:0 .4em;color:#7f7f7f}.chroma .k{color:#000;font-weight:700}.chroma .kc{color:#000;font-weight:700}.chroma .kd{color:#000;font-weight:700}.chroma .kn{color:#000;font-weight:700}.chroma .kp{color:#000;font-weight:700}.chroma .kr{color:#000;font-weight:700}.chroma .kt{color:#458;font-weight:700}.chroma .na{color:teal}.chroma .nb{color:#0086b3}.chroma .bp{color:#999}.chroma .nc{color:#458;font-weight:700}.chroma .no{color:teal}.chroma .nd{color:#3c5d5d;font-weight:700}.chroma .ni{color:purple}.chroma .ne{color:#900;font-weight:700}.chroma .nf{color:#900;font-weight:700}.chroma .nl{color:#900;font-weight:700}.chroma .nn{color:#555}.chroma .nt{color:navy}.chroma .nv{color:teal}.chroma .vc{color:teal}.chroma .vg{color:teal}.chroma .vi{color:teal}.chroma .s{color:#d14}.chroma .sa{color:#d14}.chroma .sb{color:#d14}.chroma .sc{color:#d14}.chroma .dl{color:#d14}.chroma .sd{color:#d14}.chroma .s2{color:#d14}.chroma .se{color:#d14}.chroma .sh{color:#d14}.chroma .si{color:#d14}.chroma .sx{color:#d14}.chroma .sr{color:#009926}.chroma .s1{color:#d14}.chroma .ss{color:#990073}.chroma .m{color:#099}.chroma .mb{color:#099}.chroma .mf{color:#099}.chroma .mh{color:#099}.chroma .mi{color:#099}.chroma .il{color:#099}.chroma .mo{color:#099}.chroma .o{color:#000;font-weight:700}.chroma .ow{color:#000;font-weight:700}.chroma .c{color:#998;font-style:italic}.chroma .ch{color:#998;font-style:italic}.chroma .cm{color:#998;font-style:italic}.chroma .c1{color:#998;font-style:italic}.chroma .cs{color:#999;font-weight:700;font-style:italic}.chroma .cp{color:#999;font-weight:700;font-style:italic}.chroma .cpf{color:#999;font-weight:700;font-style:italic}.chroma .gd{color:#000;background-color:#fdd}.chroma .ge{color:#000;font-style:italic}.chroma .gr{color:#a00}.chroma .gh{color:#999}.chroma .gi{color:#000;background-color:#dfd}.chroma .go{color:#888}.chroma .gp{color:#555}.chroma .gs{font-weight:700}.chroma .gu{color:#aaa}.chroma .gt{color:#a00}.chroma .gl{text-decoration:underline}.chroma .w{color:#bbb}body{display:grid;grid-template-columns:repeat(12,1fr);grid-gap:1em 1em;font-size:1.2em;font-family:Courier New;line-height:1.6;color:#000}.header,.main,.footer{grid-column:4/span 6}.header{margin-top:1em}.header__menu{margin:0;padding:0;display:flex;overflow:auto;justify-content:flex-start;border:1px solid #333}.header__menu a{font-size:1.2em;white-space:nowrap;border-bottom:none}.header__menu a:hover{color:#d14}.header__menu__logo{line-height:0}.header__menu__logo svg{width:75px;height:75px;min-width:75px;min-height:75px}.header__menu__list{display:flex;flex-grow:1;flex-wrap:nowrap;align-items:center;justify-content:space-around}.header__menu__list li{padding:0 1em;display:inline}.main{min-width:0;min-height:80vh}.main .pagination{margin:3em auto 2em;display:flex;justify-content:space-between}.footer{display:flex;justify-content:space-between;flex-wrap:wrap}h1{font-size:3.5rem}h2{font-size:2.5rem}h3{font-size:2rem}h4{font-size:1.5rem}a{color:inherit;text-decoration:none;transition:background .3s;border-bottom:2px dashed #37474f}a:hover{border-color:#d14}.button{padding:.5em .75em;font-size:1.2em;text-align:center;border:1px solid #000;box-shadow:7px 7px 0 0 #333}.button:hover{color:#d14;border:1px solid #000;transform:translate(4px,4px);box-shadow:3px 3px 0 0 #333}li{margin-top:.25em}pre,code{font-family:lucida console,Monaco,monospace;font-size:12pt;background-color:#f1f1f1}blockquote{margin:inherit auto;margin-left:1em;padding:1em;border-left:5px solid #999}blockquote:before{display:none}blockquote:not(:first-of-type){margin-top:.5em}blockquote p{color:#555;font-size:1.25em;font-family:times new roman,serif}.figure{width:100%;max-width:100%}.figure--with-caption{display:flex;border-top:6px solid #333}.figure__image--with-caption{min-width:70%}.figure__caption{background-color:#333;color:#fff;font-weight:700;padding:.5em 1em;height:min-content;word-wrap:break-word}.post-it{width:100%;padding:1.5em}.post-it--tip{background-color:#fffacd}.post-it--info{background-color:azure}.post-it--danger{background-color:#ffcccb}.post-it--success{background-color:#d0f0c0}.post-it__title{font-weight:700;font-size:1.5em}.post-it__content{margin-top:1em}.product{width:100%;display:flex;justify-content:space-between;padding:1.5em;border:1px solid #333}.product__image{margin:auto;width:100%;min-width:250px;max-width:400px}.product__content{margin-left:2em;align-self:center;display:flex;flex-direction:column}.product__title{font-weight:700;font-size:1.5rem}.product__description{margin-top:1em}.product__cta{margin-top:1em}.social-share{display:flex;align-self:center;align-items:center}.social-share__button{margin:0 .5em;border-radius:50%;background-size:60%}#tags{margin:0;padding:0}#tags li{display:inline}.content{width:100%}.content>*{margin-top:1.5em}.content>h1{margin-top:.5em}.content pre{overflow:auto;padding:.5em}.content code{padding:.1em}.content table{display:block;overflow-x:auto;border-collapse:collapse}.content table td,.content table th{border:1px solid #ddd}.content table td{padding:.5em 1em}.content table th{padding:1em 2em;background-color:#333;color:#fff}.content table tr:nth-child(even){background-color:#f1f1f1}.content table tr:hover{background-color:#ddd}.content .highlight .chroma{background-color:#f1f1f1}.content .under-title{display:flex;flex-wrap:wrap;justify-content:space-between;font-size:1rem}.content .under-title__info,.content .under-title__social-share{align-self:center}.content .ad{display:flex;margin:1rem auto;align-content:center;width:min-content;height:min-content;min-width:320px;min-height:320px;border:1px solid #333}.content .ad__fallback{display:flex;align-items:center}.content .ad__fallback p{margin:auto}.content .author{display:flex;flex-direction:column;align-items:center;background-color:#f1f1f1;padding:1.5rem}.content .author>*:not(:first-child){margin-top:1rem}.content .author__name{font-weight:700;font-size:1.5em}.content .author__image{border-radius:100px}.content .author__bio,.content .author__cta{text-align:center}.content .author__cta{font-size:1.25em}.summary:not(:first-of-type) h2{margin-top:2.5em}.summary>*{margin-top:1.25em}.summary__title{text-align:center}.summary .button{display:block;margin:inherit 1em}@media(max-width:1200px){body{grid-gap:0}.main,.header,.footer{grid-column:1/span 12}.main,.footer{margin:1em .75em 0 .5em}.header{margin:0}.header__menu{border:none;border-bottom:1px solid #333}h1{font-size:2.5rem}h2{font-size:2rem}h3{font-size:1.66rem}h4{font-size:1.25rem}.post-it{margin-left:0;margin-right:0}}@media(max-width:600px){.under-title__social-share{width:100%;margin-top:1.5em;justify-content:space-between}.figure{flex-direction:column-reverse}.figure--with-caption{border-top:none}.figure__caption{position:relative;max-width:100%}.product{flex-wrap:wrap}.product__content{margin-left:unset;text-align:center}.product__title{margin-top:1em}}
    
    
        
            
        
    
</style><script async src="https://cdn.ampproject.org/v0.js"></script><script async custom-element="amp-ad" src="https://cdn.ampproject.org/v0/amp-ad-0.1.js"></script><script async custom-element="amp-anim" src="https://cdn.ampproject.org/v0/amp-anim-0.1.js"></script><script async custom-element="amp-iframe" src="https://cdn.ampproject.org/v0/amp-iframe-0.1.js"></script><script async custom-element="amp-analytics" src="https://cdn.ampproject.org/v0/amp-analytics-0.1.js"></script><script async custom-element="amp-social-share" src="https://cdn.ampproject.org/v0/amp-social-share-0.1.js"></script><script async custom-element="amp-install-serviceworker" src="https://cdn.ampproject.org/v0/amp-install-serviceworker-0.1.js"></script>


    
        
        
    
</head>
	<body>
		<amp-auto-ads type="adsense"
        data-ad-client="ca-pub-7855172652409324">
		</amp-auto-ads><amp-install-serviceworker
  src="https://huhu.blue/sw.js"
  data-iframe-src="https://huhu.blue/install-sw.html"
  layout="nodisplay">
</amp-install-serviceworker>
  <amp-analytics type="gtag" data-credentials="include">
    <script type="application/json">
      {
        "vars": {
          "gtag_id": "UA-161442409-1",
          "config": {
            "UA-161442409-1": { "groups": "default" }
          }
        },
        "triggers": {
          "trackPageview": {
            "on": "visible",
            "request": "pageview"
          }
        }
      }
    </script>
  </amp-analytics>





  
  
  

  
  
  
    
  

  
  
  


<script type="application/ld+json">
  {
    "@context": "http://schema.org",
    "@type": "BreadcrumbList",
    "itemListElement": [
      
        
        {
          "@type": "ListItem",
          "position":  1 ,
          "item": {
            "@id": "https:\/\/huhu.blue",
            "name": "主页"
          }
        }
      
        ,
        {
          "@type": "ListItem",
          "position":  2 ,
          "item": {
            "@id": "https:\/\/huhu.blue\/how-to-combine-cloudflare-with-ipv6-only-vps\/",
            "name": "How to combine cloudflare with ipv6 only vps"
          }
        }
       ]
  }
</script><script type="application/ld+json">
  {
    "@context":"http://schema.org",
    "@type": "BlogPosting",
    "image": "https:\/\/huhu.blue",
    "url": "https:\/\/huhu.blue\/how-to-combine-cloudflare-with-ipv6-only-vps\/",
    "headline": "怎样在ipv6 only 的vps上安装v2ray\x2bws\x2bTLS\x2bCDN？",
    "alternativeHeadline": "怎样在ipv6 only 的vps上安装v2ray\x2bws\x2bTLS\x2bCDN？",
    "dateCreated": "2020-03-23T08:05:23",
    "datePublished": "2020-03-23T08:05:23",
    "dateModified": "2020-03-23T08:05:23",
    "inLanguage": "zh",
    "isFamilyFriendly": "true",
    "copyrightYear": "2020",
    "copyrightHolder": "HuHu",
    "accountablePerson": {
      "@type": "Person",
      "name": "HuHu",
      "url": "\/"
    },
    "author": {
      "@type": "Person",
      "name": "HuHu",
      "url": "https:\/\/huhu.blue\/",
      "image": "https:\/\/cdn.jsdelivr.net\/gh\/Scaleya\/jsdelivr\/huhu.blue\/avatar\/avatar.png",
      "description": "电报群可以联系我！"
    },
    "creator": {
      "@type": "Person",
      "name": "HuHu",
      "url": "https:\/\/huhu.blue\/",
      "image": "https:\/\/cdn.jsdelivr.net\/gh\/Scaleya\/jsdelivr\/huhu.blue\/avatar\/avatar.png",
      "description": "电报群可以联系我！"
    },
    "publisher": {
      "@type": "Organization",
      "name": "HuHu",
      "url": "https:\/\/huhu.blue",
      "logo": {
        "@type": "ImageObject",
        "url": "https:\/\/cdn.jsdelivr.net\/gh\/Scaleya\/jsdelivr\/huhu.blue\/avatar\/portrait.png",
        "width":"600",
        "height":"60"
      }
    },
    "mainEntityOfPage": "https:\/\/huhu.blue\/how-to-combine-cloudflare-with-ipv6-only-vps\/",
    "keywords": "[\"ipv6 only\",\"ws+tls+CDN\",\"V2Ray\"]",
    "genre": "[\"ipv6 only\",\"ws+tls+CDN\",\"V2Ray\"]",
    "articleSection": "HuHu"
  }
</script><header class="header"><nav class="header__menu">
    <a class="header__menu__logo" data-rel="prefetch" href="https://huhu.blue" aria-label="返回主页"><svg width="256" height="256" viewBox="0 0 256 256" version="1.1" xmlns="http://www.w3.org/2000/svg">
 <rect x="2.0205e-9" y="2.0205e-9" width="259.25" height="261.42" fill="#333" stroke-width="1.0148"/>
 <path d="m171.89 116.28-53.696 89.36h-9.728l9.617-58.227-30.2 0.047c-2.684 0-4.855-2.172-4.855-4.855 0-1.152 1.07-3.102 1.07-3.102l53.52-89.254 9.9 0.043-9.86 58.317 30.413-0.043c2.684 0 4.855 2.172 4.855 4.855 0 1.088-0.427 2.044-1.033 2.854l4e-3 4e-3z" fill="#fff" fill-rule="evenodd"/>
</svg>
</a><ul class="header__menu__list">
    
        
        <li>
            <a href="https://huhu.blue"
                  rel="nofollow noopener noreferrer" >
                <span>主页</span>
            </a>
        </li>
    
</ul></nav></header>
		<main class="main">
	<article class="content">
		

<h1 id="怎样在ipv6-only-的vps上安装v2ray-ws-tls-cdn">怎样在ipv6 only 的vps上安装v2ray+ws+TLS+CDN？</h1>

<section class="under-title">
    <div class="under-title__info">
        <time datetime="2020-03-23T08:05:23">
            
            
            2020-03-23
        </time>
         作者:</li>&nbsp; HuHu 
        
        <ul id="tags">
            <li>标签:</li>&nbsp;
            
                
                
                    <li><a href="https://huhu.blue/tags/ipv6-only/" data-rel="prefetch">ipv6 only</a></li>
                
            
                
                
                    <li><a href="https://huhu.blue/tags/ws&#43;tls&#43;cdn/" data-rel="prefetch">ws&#43;tls&#43;CDN</a></li>
                
            
                
                
                    <li><a href="https://huhu.blue/tags/v2ray/" data-rel="prefetch">V2Ray</a></li>
                
            
        </ul>
    </div>
    <div class="under-title__social-share social-share"><amp-social-share class="social-share__button"
    aria-label="Share content" type="system" width="50" height="50"></amp-social-share>
</div>
</section>

<p>本地网络没有ipv6但是有台免费的ipv6 only vps怎么使用啊，这里介绍使用cloudflare的cdn让你的本地可以使用这种ipv6 only vps的网络。</p>

<div class="post-it  post-it--success ">
     <div class="post-it__title">Success! 🎉</div>
    <div class="post-it__content">
        <del>不过我发现这种方法仍然不能正常访问只用ipv4的网站。</del>用下面的方法可以解决，但是ipv4可能是黑名单吧！？
    </div>
</div>

<div class="highlight"><div class="chroma">
<table class="lntable"><tr><td class="lntd">
<pre class="chroma"><code><span class="lnt">1
</span><span class="lnt">2
</span><span class="lnt">3
</span><span class="lnt">4
</span><span class="lnt">5
</span><span class="lnt">6
</span><span class="lnt">7
</span><span class="lnt">8
</span><span class="lnt">9
</span></code></pre></td>
<td class="lntd">
<pre class="chroma"><code class="language-bash" data-lang="bash"><span class="nb">echo</span> <span class="s2">&#34;
</span><span class="s2">nameserver 2001:67c:2b0::4
</span><span class="s2">nameserver 2001:67c:2b0::6 &#34;</span> &gt; /etc/resolv.conf

<span class="c1"># 随便选一个</span>

<span class="nb">echo</span> <span class="s2">&#34;
</span><span class="s2">nameserver 2001:67c:27e4:15::6411
</span><span class="s2">nameserver 2001:67c:27e4::64 &#34;</span> &gt; /etc/resolv.conf</code></pre></td></tr></table>
</div>
</div>

<p><b>目录:</b>
<nav id="TableOfContents">
<ul>
<li><a href="#怎样在ipv6-only-的vps上安装v2ray-ws-tls-cdn">怎样在ipv6 only 的vps上安装v2ray+ws+TLS+CDN？</a>
<ul>
<li><a href="#ssh连接到ipv6-only-vps">ssh连接到ipv6 only vps</a></li>
<li><a href="#ipv6-only-一键安装v2ray脚本">ipv6 only 一键安装v2ray脚本</a></li>
<li><a href="#修改v2ray配置文件">修改v2ray配置文件</a></li>
<li><a href="#ws-tls配置示例">ws+tls配置示例</a></li>
<li><a href="#证书">证书</a></li>
<li><a href="#ws-tls-完整配置示例">ws+tls 完整配置示例</a></li>
<li><a href="#开启自启-启动-状态">开启自启 启动 状态</a></li>
</ul></li>
</ul>
</nav></p>

<div class="post-it  post-it--info ">
     <div class="post-it__title">Info! 💬</div>
    <div class="post-it__content">
        事先将域名添加一个AAAA解析指向自己的ipv6地址，这里以<code>scaleya.xyz</code>为例
    </div>
</div>

<h2 id="ssh连接到ipv6-only-vps">ssh连接到ipv6 only vps</h2>

<ul>
<li>如果没有ipv6环境可以使用双栈vps做跳板连接到
<div class="highlight"><div class="chroma">
<table class="lntable"><tr><td class="lntd">
<pre class="chroma"><code><span class="lnt">1
</span></code></pre></td>
<td class="lntd">
<pre class="chroma"><code class="language-bash" data-lang="bash">ssh root@2001:19f0:5401:1741:5400:02ff:fea2:2783</code></pre></td></tr></table>
</div>
</div></li>
</ul>

<h2 id="ipv6-only-一键安装v2ray脚本">ipv6 only 一键安装v2ray脚本</h2>

<ul>
<li>输入以下命令 记住uuid 和 port
<div class="highlight"><div class="chroma">
<table class="lntable"><tr><td class="lntd">
<pre class="chroma"><code><span class="lnt">1
</span><span class="lnt">2
</span><span class="lnt">3
</span><span class="lnt">4
</span></code></pre></td>
<td class="lntd">
<pre class="chroma"><code class="language-bash" data-lang="bash">wget scaleya.com/v2ray.sh
bash v2ray.sh
<span class="c1"># PORT:20097 后面要改成443</span>
<span class="c1"># UUID:972ddc4e-522c-4d66-8616-358c1aa5d132</span></code></pre></td></tr></table>
</div>
</div></li>
</ul>

<h2 id="修改v2ray配置文件">修改v2ray配置文件</h2>

<ul>
<li>套用cf的cdn让ipv6 only 也能用在ipv4上
<div class="highlight"><div class="chroma">
<table class="lntable"><tr><td class="lntd">
<pre class="chroma"><code><span class="lnt">1
</span><span class="lnt">2
</span></code></pre></td>
<td class="lntd">
<pre class="chroma"><code class="language-bash" data-lang="bash">nano /etc/v2ray/config.json
<span class="c1"># 修改使用ws并配置tls</span></code></pre></td></tr></table>
</div>
</div></li>
</ul>

<h2 id="ws-tls配置示例">ws+tls配置示例</h2>

<ul>
<li>
<div class="highlight"><div class="chroma">
<table class="lntable"><tr><td class="lntd">
<pre class="chroma"><code><span class="lnt"> 1
</span><span class="lnt"> 2
</span><span class="lnt"> 3
</span><span class="hl"><span class="lnt"> 4
</span></span><span class="lnt"> 5
</span><span class="hl"><span class="lnt"> 6
</span></span><span class="lnt"> 7
</span><span class="lnt"> 8
</span><span class="hl"><span class="lnt"> 9
</span></span><span class="hl"><span class="lnt">10
</span></span><span class="lnt">11
</span><span class="lnt">12
</span><span class="lnt">13
</span></code></pre></td>
<td class="lntd">
<pre class="chroma"><code class="language-bash" data-lang="bash"><span class="s2">&#34;streamSettings&#34;</span>: <span class="o">{</span>
        <span class="s2">&#34;network&#34;</span>:<span class="s2">&#34;ws&#34;</span>,
        <span class="s2">&#34;wsSettings&#34;</span>: <span class="o">{</span>
<span class="hl">          <span class="s2">&#34;path&#34;</span>: <span class="s2">&#34;/&#34;</span>
</span>        <span class="o">}</span>,
<span class="hl">        <span class="s2">&#34;security&#34;</span>: <span class="s2">&#34;tls&#34;</span>,
</span>        <span class="s2">&#34;tlsSettings&#34;</span>:<span class="o">{</span>
          <span class="s2">&#34;certificates&#34;</span>: <span class="o">[{</span>
<span class="hl">            <span class="s2">&#34;certificateFile&#34;</span>: <span class="s2">&#34;/etc/v2ray/v2ray.crt&#34;</span>,
</span><span class="hl">            <span class="s2">&#34;keyFile&#34;</span>: <span class="s2">&#34;/etc/v2ray/v2ray.key&#34;</span>
</span>            <span class="o">}]</span>
        <span class="o">}</span>
    <span class="o">}</span></code></pre></td></tr></table>
</div>
</div></li>
</ul>

<h2 id="证书">证书</h2>

<ul>
<li>证书来自cloudflare的15年免费证书</li>
<li>类型 ECDSA</li>
<li>分别存储为 /etc/v2ray/v2ray.crt</li>
<li>/etc/v2ray/v2ray.key</li>
</ul>

<!-- 
-----BEGIN CERTIFICATE-----
MIIDIjCCAsigAwIBAgIUcZFRxo85HZTbjzGyhPoYgxu9JLwwCgYIKoZIzj0EAwIw
gY8xCzAJBgNVBAYTAlVTMRMwEQYDVQQIEwpDYWxpZm9ybmlhMRYwFAYDVQQHEw1T
YW4gRnJhbmNpc2NvMRkwFwYDVQQKExBDbG91ZEZsYXJlLCBJbmMuMTgwNgYDVQQL
Ey9DbG91ZEZsYXJlIE9yaWdpbiBTU0wgRUNDIENlcnRpZmljYXRlIEF1dGhvcml0
eTAeFw0yMDAzMjMwMDM1MDBaFw0zNTAzMjAwMDM1MDBaMGIxGTAXBgNVBAoTEENs
b3VkRmxhcmUsIEluYy4xHTAbBgNVBAsTFENsb3VkRmxhcmUgT3JpZ2luIENBMSYw
JAYDVQQDEx1DbG91ZEZsYXJlIE9yaWdpbiBDZXJ0aWZpY2F0ZTBZMBMGByqGSM49
AgEGCCqGSM49AwEHA0IABCKPZLehlsfO0qRPHjroHafoUzvicbkBRRTQNmd//syO
R6gvAEse2Wx2rS2SaqlQUYczf89Vkx/mWaMeQWSC3zejggEsMIIBKDAOBgNVHQ8B
Af8EBAMCBaAwHQYDVR0lBBYwFAYIKwYBBQUHAwIGCCsGAQUFBwMBMAwGA1UdEwEB
/wQCMAAwHQYDVR0OBBYEFAs9slT28bthL/uHpGpzQIQExe/XMB8GA1UdIwQYMBaA
FIUwXTsqcNTt1ZJnB/3rObQaDjinMEQGCCsGAQUFBwEBBDgwNjA0BggrBgEFBQcw
AYYoaHR0cDovL29jc3AuY2xvdWRmbGFyZS5jb20vb3JpZ2luX2VjY19jYTAlBgNV
HREEHjAcgg0qLnNjYWxleWEueHl6ggtzY2FsZXlhLnh5ejA8BgNVHR8ENTAzMDGg
L6AthitodHRwOi8vY3JsLmNsb3VkZmxhcmUuY29tL29yaWdpbl9lY2NfY2EuY3Js
MAoGCCqGSM49BAMCA0gAMEUCIB4FRKSPGuoNwp2bWjLU5lxzioes9N/f1ad6bfAd
AN18AiEAnQ2ijS/KZNbkIyCGwPpEVpt7lLHJDyzOTZoS6xkG7o4=
-----END CERTIFICATE-----


-----BEGIN PRIVATE KEY-----
MIGHAgEAMBMGByqGSM49AgEGCCqGSM49AwEHBG0wawIBAQQgoOlKzAkXz7KL2GS/
Au0/3DFPnSNPObJsOZIY69WEemuhRANCAAQij2S3oZbHztKkTx466B2n6FM74nG5
AUUU0DZnf/7MjkeoLwBLHtlsdq0tkmqpUFGHM3/PVZMf5lmjHkFkgt83
-----END PRIVATE KEY-----




 -->


    
        <fieldset class="ad">
            <legend><b>#ad</b></legend>
            <amp-ad type="adsense"
                
                
                 width="320"
                 height="320"
                 layout="fixed"
                 data-ad-slot="9425131909" 
                data-ad-client="ca-pub-7855172652409324">
                <div class="ad__fallback" fallback><p>无广告显示!</p></div>
            </amp-ad>
        </fieldset>
    


<h2 id="ws-tls-完整配置示例">ws+tls 完整配置示例</h2>

<div class="post-it  post-it--tip ">
     <div class="post-it__title">Warning! 🚨</div>
    <div class="post-it__content">
        line 3 端口必须 443
line 13 尾巴要加上一个 ,
    </div>
</div>

<div class="highlight"><div class="chroma">
<table class="lntable"><tr><td class="lntd">
<pre class="chroma"><code><span class="lnt"> 1
</span><span class="lnt"> 2
</span><span class="hl"><span class="lnt"> 3
</span></span><span class="lnt"> 4
</span><span class="lnt"> 5
</span><span class="lnt"> 6
</span><span class="lnt"> 7
</span><span class="lnt"> 8
</span><span class="lnt"> 9
</span><span class="lnt">10
</span><span class="lnt">11
</span><span class="lnt">12
</span><span class="hl"><span class="lnt">13
</span></span><span class="hl"><span class="lnt">14
</span></span><span class="hl"><span class="lnt">15
</span></span><span class="hl"><span class="lnt">16
</span></span><span class="hl"><span class="lnt">17
</span></span><span class="hl"><span class="lnt">18
</span></span><span class="hl"><span class="lnt">19
</span></span><span class="hl"><span class="lnt">20
</span></span><span class="hl"><span class="lnt">21
</span></span><span class="hl"><span class="lnt">22
</span></span><span class="hl"><span class="lnt">23
</span></span><span class="hl"><span class="lnt">24
</span></span><span class="hl"><span class="lnt">25
</span></span><span class="hl"><span class="lnt">26
</span></span><span class="lnt">27
</span><span class="lnt">28
</span><span class="lnt">29
</span><span class="lnt">30
</span><span class="lnt">31
</span><span class="lnt">32
</span><span class="lnt">33
</span><span class="lnt">34
</span><span class="lnt">35
</span><span class="lnt">36
</span><span class="lnt">37
</span><span class="lnt">38
</span><span class="lnt">39
</span><span class="lnt">40
</span><span class="lnt">41
</span><span class="lnt">42
</span><span class="lnt">43
</span><span class="lnt">44
</span><span class="lnt">45
</span></code></pre></td>
<td class="lntd">
<pre class="chroma"><code class="language-bash" data-lang="bash"><span class="o">{</span>
  <span class="s2">&#34;inbounds&#34;</span>: <span class="o">[{</span>
<span class="hl">    <span class="s2">&#34;port&#34;</span>: 443,
</span>    <span class="s2">&#34;protocol&#34;</span>: <span class="s2">&#34;vmess&#34;</span>,
    <span class="s2">&#34;settings&#34;</span>: <span class="o">{</span>
      <span class="s2">&#34;clients&#34;</span>: <span class="o">[</span>
        <span class="o">{</span>
          <span class="s2">&#34;id&#34;</span>: <span class="s2">&#34;972ddc4e-522c-4d66-8616-358c1aa5d132&#34;</span>,
          <span class="s2">&#34;level&#34;</span>: 1,
          <span class="s2">&#34;alterId&#34;</span>: <span class="m">64</span>
        <span class="o">}</span>
      <span class="o">]</span>
<span class="hl">    <span class="o">}</span>,
</span><span class="hl">    <span class="s2">&#34;streamSettings&#34;</span>: <span class="o">{</span>
</span><span class="hl">        <span class="s2">&#34;network&#34;</span>:<span class="s2">&#34;ws&#34;</span>,
</span><span class="hl">        <span class="s2">&#34;wsSettings&#34;</span>: <span class="o">{</span>
</span><span class="hl">          <span class="s2">&#34;path&#34;</span>: <span class="s2">&#34;/&#34;</span>
</span><span class="hl">        <span class="o">}</span>,
</span><span class="hl">        <span class="s2">&#34;security&#34;</span>: <span class="s2">&#34;tls&#34;</span>,
</span><span class="hl">        <span class="s2">&#34;tlsSettings&#34;</span>:<span class="o">{</span>
</span><span class="hl">          <span class="s2">&#34;certificates&#34;</span>: <span class="o">[{</span>
</span><span class="hl">            <span class="s2">&#34;certificateFile&#34;</span>: <span class="s2">&#34;/etc/v2ray/v2ray.crt&#34;</span>,
</span><span class="hl">            <span class="s2">&#34;keyFile&#34;</span>: <span class="s2">&#34;/etc/v2ray/v2ray.key&#34;</span>
</span><span class="hl">            <span class="o">}]</span>
</span><span class="hl">        <span class="o">}</span>
</span><span class="hl">    <span class="o">}</span>
</span>  <span class="o">}]</span>,
  <span class="s2">&#34;outbounds&#34;</span>: <span class="o">[{</span>
    <span class="s2">&#34;protocol&#34;</span>: <span class="s2">&#34;freedom&#34;</span>,
    <span class="s2">&#34;settings&#34;</span>: <span class="o">{}</span>
  <span class="o">}</span>,<span class="o">{</span>
    <span class="s2">&#34;protocol&#34;</span>: <span class="s2">&#34;blackhole&#34;</span>,
    <span class="s2">&#34;settings&#34;</span>: <span class="o">{}</span>,
    <span class="s2">&#34;tag&#34;</span>: <span class="s2">&#34;blocked&#34;</span>
  <span class="o">}]</span>,
  <span class="s2">&#34;routing&#34;</span>: <span class="o">{</span>
    <span class="s2">&#34;rules&#34;</span>: <span class="o">[</span>
      <span class="o">{</span>
        <span class="s2">&#34;type&#34;</span>: <span class="s2">&#34;field&#34;</span>,
        <span class="s2">&#34;ip&#34;</span>: <span class="o">[</span><span class="s2">&#34;geoip:private&#34;</span><span class="o">]</span>,
        <span class="s2">&#34;outboundTag&#34;</span>: <span class="s2">&#34;blocked&#34;</span>
      <span class="o">}</span>
    <span class="o">]</span>
  <span class="o">}</span>
<span class="o">}</span></code></pre></td></tr></table>
</div>
</div>

<div class="post-it  post-it--danger ">
     <div class="post-it__title">Danger! 💀</div>
    <div class="post-it__content">
        <p>没有伪装站，无法使用
<div class="highlight"><div class="chroma">
<table class="lntable"><tr><td class="lntd">
<pre class="chroma"><code><span class="lnt">1
</span><span class="lnt">2
</span><span class="lnt">3
</span></code></pre></td>
<td class="lntd">
<pre class="chroma"><code class="language-bash" data-lang="bash"><span class="s2">&#34;headers&#34;</span>: <span class="o">{</span>
    <span class="s2">&#34;Host&#34;</span>: <span class="s2">&#34;v2ray.com&#34;</span>
    <span class="o">}</span></code></pre></td></tr></table>
</div>
</div></p>

    </div>
</div>

<h2 id="开启自启-启动-状态">开启自启 启动 状态</h2>

<div class="highlight"><div class="chroma">
<table class="lntable"><tr><td class="lntd">
<pre class="chroma"><code><span class="lnt">1
</span><span class="lnt">2
</span></code></pre></td>
<td class="lntd">
<pre class="chroma"><code class="language-bash" data-lang="bash">service v2ray start
service v2ray status</code></pre></td></tr></table>
</div>
</div>


    <h2 class="related-content__title">相关阅读 📖</h2>
    
        <p class="related-content__item"><a href="https://huhu.blue/how-to-deploy-v2ray-on-ipv6-only-vps/" data-rel="prefetch">怎样在IPv6 Only VPS上部署V2Ray？</a></p>
    

    <section class="author">
        
            <p class="author__name">HuHu</p>
        
        
            <amp-img class="author__image"
                src="https://cdn.jsdelivr.net/gh/Scaleya/jsdelivr/huhu.blue/avatar/avatar.png"
                layout="fixed" height="200" width="200"></amp-img>
        
        
            <p class="author__bio">电报群可以联系我！</p>
        
        <p class="author__cta">If you liked it share and repost!</p>
        <div class="social-share"><amp-social-share class="social-share__button"
    aria-label="Share content" type="system" width="50" height="50"></amp-social-share>
</div>
    </section>
</article>

		</main>
		<footer class="footer"><div class="footer__copyright">© HuHu 2020</div>
</footer>
	</body>
</html>
