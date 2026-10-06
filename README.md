2026年10月6日
参考视频：https://www.youtube.com/watch?v=WEDHp7pNDaA \
参考blog：https://blog.imxiaohe.com/2026/09/123.html

1.Actions 执行报错修正  
Node.js 20 弃用警告
# 旧版本（会报这个警告）
- uses: actions/checkout@v4
- uses: actions/setup-python@v5

# 改成新版
- uses: actions/checkout@v5
- uses: actions/setup-python@v6

2.修正部署中yml文件的CHECK_WORKER变量，
因源引用的YTB-小何爱分享的检测worker地址，用户过多导致Action执行时无法正常访问，报522错误，
个人认为视频中第一个部署的就可以用到这里，毕竟视频中只看到了部署这个，但是没看到哪里使用，虽然vpngate.py修正过变量是指向这个URL，但是部署执行的yml中的还是YTB-小何爱分享，故此修正这里指向自己的URL(即raspy-term-e2fd workers)

3.在 vpngate.py 中修改三处核心配置
3.1 替换 Worker 测速检测端
变量WORKER_CHECK_URL，修正此变量URL是自己部署在cloudflare中raspy-term-e2fd的URL
3.2 替换 Cloudflare 优选域名池
变量EDGE_HOSTS，要求每个地址后必须带上 :443 端口
3.3 必须配置用户自己的 edgetunnel 节点信息
这个就是部署在cloudflare中square-hill-0b71e2df workers相关变量，分别是EDT_UUID(填入你自己edgetunnel的UUID)、EDT_DOMAIN(填入你自己edgetunnel绑定的节点域名)

4.两大访问地址
4.1 页面一：节点前端展示与下载页面（GitHub Pages 网址）
https://你的GitHub用户名.github.io/仓库名/                
即：https://exileme.github.io/raspy-term-e2fd-gate/
4.2 页面二：复制内容并粘贴到 EDG 后台的专用网页 ※打开此页面后，可直接全选复制页面中的节点配置文本，然后粘贴进 EDG 后台系统(部署的cloudflare中square-hill-0b71e2df)
https://你的GitHub用户名.github.io/仓库名/hosts.txt      
即：https://exileme.github.io/raspy-term-e2fd-gate/hosts.txt 
