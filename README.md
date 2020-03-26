# Shell
V2RAY-233blog
 <code>bash &lt;(curl -s -L https://git.io/v2ray.sh)
</code>
如果提示 curl: command not found ，那是因为你的 VPS 没装 Curl
ubuntu/debian 系统安装 Curl 方法: apt-get update -y && apt-get install curl -y
centos 系统安装 Curl 方法: yum update -y && yum install curl -y
安装好 curl 之后就能安装脚本了
