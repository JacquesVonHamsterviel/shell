<!DOCTYPE html>
<html ⚡ lang="zh">
<head></head>
	<body>
<h1 id="怎样在ipv6-only-的vps上安装v2ray-ws-tls-cdn">怎样在ipv6 only 的vps上安装v2ray+ws+TLS+CDN？</h1>


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

	</body>
</html>
