# Shell
<p>V2RAY-233blog脚本</p>
 <code>bash &lt;(curl -s -L https://raw.githubusercontent.com/JacquesVonHamsterviel/shell/master/v2ray.sh)
</code>
<blockquote>
<p>如果提示 curl: command not found ，那是因为你的 VPS 没装 Curl<br>
ubuntu/debian 系统安装 Curl 方法: <code>apt-get update -y &amp;&amp; apt-get install curl -y</code><br>
centos 系统安装 Curl 方法: <code>yum update -y &amp;&amp; yum install curl -y</code><br>
安装好 curl 之后就能安装脚本了</p>
</blockquote>
<p>V2ray-ipv6安装脚本</p>
<p>Cmd连接ipv6服务器</p><code>ssh root @ipv6地址</code>
<code>wget https://raw.githubusercontent.com/JacquesVonHamsterviel/shell/master/v2ray-ipv6.sh</code>
<code>bash v2ray-ipv6.sh -f</code>
<code>start v2ray</code>
<p>V2ray启动状态</p><code>status v2ray</code>
