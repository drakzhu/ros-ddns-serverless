## ROS上设置DDNS
网上看的教程中，都是用的他们提供的接口服务，不太敢用，所以还是自己搭一个比较靠谱

## 调试
```
git clone https://github.com/AlanLang/ros-ddns-serverless.git
yarn
yarn vercel dev
```

## 部署
直接部署在vercel上即可

## 使用
添加ROS脚本，记得请求地址替换成自己的
输入时最好把中文注释给删了
```
:local identifier "" #id
:local secret "" #token
:local type 解析类型，默认为A
:local record 需要解析的域名 
:local pppoe "pppoe-out1" #确定你的路由器的网口名称
:local ipaddr [/ip address get [/ip address find interface=$pppoe] address]
:set ipaddr [:pick $ipaddr 0 ([len $ipaddr] -3)]
:global aliip
:if ($ipaddr != $aliip) do={
    :local result [/tool fetch url="https://ros-ddns-serverless.vercel.app/api/aliyun?identifier=$identifier&secret=$secret&record=$record&type=$type&ip=$ipaddr" as-value output=user];
    :set aliip $ipaddr
}
```
至于怎么使用这个脚本，是定时运行还是wan口重新拨号后自动运行就看你自己怎么设置了，这边不赘述。
