# v2ray-agent：XHTTP + TLS 公网端口 1–50000

基于 [mack-a/v2ray-agent](https://github.com/mack-a/v2ray-agent) 的安装脚本修改，保留上游版权与 AGPL-3.0 许可。修改版为 `install.sh`，下载时的原始副本为 `install.upstream.sh`。

## 在 VPS 下载运行

仓库为公开仓库，无需登录 GitHub。以 root 运行以下命令，先下载为临时文件，成功后才替换 `/root/install.sh`：

```bash
curl -fL https://raw.githubusercontent.com/Makefishr/v2ray-agent-xhttp-ports/main/install.sh -o /root/install.sh.download &&
mv /root/install.sh.download /root/install.sh &&
chmod 700 /root/install.sh &&
bash /root/install.sh
```

安装菜单：`2.任意组合安装` → `1.Xray-core` → 只输入 `14`。按提示配置域名和证书，公网端口可以填写 `443` 或其他 1–50000 的空闲端口。

## 修改范围

- 第 14 项 VLESS + XHTTP + TLS 的手动公网端口范围扩展为 1–50000。
- 保留端口占用检查和对应单个端口的防火墙放行。
- 回车时仍随机选择 10000–30000。
- 前导零输入转换为十进制，例如 00443 转为 443。
- 公网端口为 45988 时，内部 XHTTP 端口改用 45989，避免自身监听冲突；其余端口仍使用内部 45988。

此修改不会开放全部 1–50000 端口。所选端口仍需空闲，云安全组需要放行对应 TCP 端口。

上游的“更新脚本”功能会下载原版并覆盖这些修改；重新下载本仓库脚本可恢复修改版。未来上游版本需要重新核对后再应用补丁。

## 验证

已完成 Bash 语法检查、1–50000 全范围输入校验、非法输入检查、配置生成及模拟端口冲突检查，结果见 `verification.txt`。差异见 `ports-1-50000.patch`。

没有运行完整安装程序，没有部署到 VPS，没有实际 Xray TLS 连接测试。
