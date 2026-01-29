SAP-SS-ARGO 是一个专为 SAP BTP Cloud Foundry 环境设计的轻量级 Node.js 应用。

众所周知，如今SAP试用版账号搭建节点完全没速度。
作为纯小白看不懂一行代码，唯有不断尝试绕过流量监测的办法。
偶然发现Shadowsocks+ws+argo协议被针对的不明显（aes弱加密方式还是会被识别，本脚本采用chacha20-ietf-poly1305加密方式）。

优点：相比VLESS方案，能够躲过SAP流量监测（肯定是暂时的，SAP这么大的公司想封节点还不跟玩似的）。
缺点：较于之前没被流量监测的时候，代理速度较慢（这不是本脚本的错，是SAP限速了）。

本脚本完全照抄“老王”大佬的 https://github.com/eooce/nodejs-argo 项目，包括二进制文件都来下载于老王的仓库，感谢老王。

较于老王的nodejs-argo项目修改了几点：
1.移除哪吒探针功能。
2.把原项目三协议：vmess、vless、trogan修改成shadowsocks。
3.AI优化了TCP/Network策略（AI自己说的）。
4.根路径返回伪造的Nginx欢迎页面（AI自己改的）。

来个免责声明吧：
本项目完全照抄，看到的自己玩玩得了。
切勿滥用，做公共代理是违法的。
切勿商用，也是违法的。
使用本项目产生的任何后果由使用者自行承担，作者不承担任何法律责任。

部署方法：会的都会。

再次感谢老王大佬，把原项目的Star点起来 https://github.com/eooce/nodejs-argo ，至于这个项目你们随意Star ⭐️
