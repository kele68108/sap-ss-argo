SAP-SS-ArgoSAP-SS-Argo 是一个专为 SAP BTP (Cloud Foundry) 环境设计的轻量级 Node.js 应用。它能够在容器内运行高性能的 Shadowsocks 节点，并通过 Cloudflare Argo Tunnel 进行内网穿透，实现高速、稳定的网络代理服务。核心亮点：相比传统的 VLESS 方案，本项目专注于 Shadowsocks 协议，通过深度优化的 TCP/Network 策略，为旧设备和特定客户端提供极佳的兼容性与连接稳定性。✨ 特性 / Features🚀 高性能优化：内置 TCP Fast Open、TCP No Delay、Keep-Alive 调优及缓冲区优化策略，显著降低延迟。🔒 安全稳定：使用 chacha20-ietf-poly1305 加密算法，配合 Argo 隧道，无需公网 IP。🎭 智能伪装：根路径返回伪造的 Nginx 欢迎页面，有效降低主动探测风险。☁️ Cloudflare Argo 集成：支持 Token 方式连接，强制 IPv4 模式，解决部分云环境 IPv6 路由不稳问题。📦 一键部署：适配 Cloud Foundry 环境，提供标准 manifest.yml 配置。🛠️ 部署指南 / Deployment1. 准备工作拥有一个 SAP BTP (Cloud Foundry) 账号。拥有一个 Cloudflare 账号（用于获取 Argo Token）。安装 Cloud Foundry CLI (cf 工具)。2. 获取 Argo Token在 Cloudflare Zero Trust 面板中创建一个新的 Tunnel，复制生成的 Token（通常以 ey... 开头）。3. 配置与部署克隆仓库Bashgit clone https://github.com/你的用户名/sap-ss-argo.git
cd sap-ss-argo
修改配置 (manifest.yml)修改项目根目录下的 manifest.yml 文件，填入你的变量：YAMLapplications:
  - name: sap-ss-argo              # 应用名称
    memory: 128M                   # 内存大小
    disk_quota: 256M
    random-route: true
    buildpacks:
      - nodejs_buildpack
    env:
      UUID: "你的密码"              # Shadowsocks 密码
      ARGO_AUTH: "eyJhIjoi..."     # 你的 Argo Tunnel Token
      ARGO_DOMAIN: "你的域名.com"    # 你的 Argo 隧道域名
      NAME: "My-Node"              # 节点名称备注
推送到服务器Bashcf login
cf push
获取订阅部署成功后，访问应用的 /sub 路径即可获取 Base64 编码的订阅链接。例如：https://你的应用域名.cfapps.ap21.hana.ondemand.com/sub⚙️ 环境变量说明 / Environment Variables变量名必填默认值说明UUID✅(随机UUID)Shadowsocks 的连接密码ARGO_AUTH✅-Cloudflare Argo Tunnel Token (长字符串)ARGO_DOMAIN✅-你在 Cloudflare Tunnel 中绑定的完整域名NAME❌Argo-SS节点显示的名称FILE_PATH❌./tmp临时文件存放路径SUB_PATH❌sub订阅信息的访问路径 (例如 /sub)⚠️ 免责声明 / Disclaimer本项目仅供学习、技术研究和科研测试使用。请勿将本项目用于任何违反当地法律法规的用途。使用本项目产生的任何后果由使用者自行承担，作者不承担任何法律责任。☕ Support如果你觉得这个项目对你有帮助，欢迎点个 Star ⭐️！
