---

## 🛠 本 fork 改动 (custom: kuaiji-vpn)

基于 upstream `2dust/v2rayNG v2.2.4`，做了 4 处改动:

1. **包名** `com.v2ray.ang` → `com.kuaiji.vpn` (applicationId)
2. **应用名** `v2rayNG` → `快极VPN` (strings.xml app_name)
3. **预装 3 条免费订阅源** (SettingsManager.preloadFreeSubscriptions):
   - Free-1 (Freedom-V2Ray, 6h 自动更新)
   - Free-2 (0xRadikal, 6h 自动更新)
   - Free-3 (wenxig, 6h 自动更新)
4. **新增 GitHub Actions 工作流**:
   - `.github/workflows/build.yml` — 云端 build APK (macOS runner 自带 Android SDK)
   - `.github/workflows/sync-nodes.yml` — 每 6 小时抓 4 个免费节点源 → 去重 → 推到 `dist/v2ray.txt`

### 自有节点池 URL (此 fork 启用 sync-nodes 后生成)
```
https://raw.githubusercontent.com/<你的用户名>/v2rayNG/main/dist/v2ray.txt
```

### Build 出 APK
- 手动: Actions tab → Build APK → Run workflow
- 自动: push 一个 tag `v*` (如 `git tag v2.2.4-kuaiji && git push --tags`)

### 修改你自己的 fork
```bash
# 1. 在 GitHub 上点 Fork
# 2. clone
git clone https://github.com/<你的用户名>/v2rayNG.git
cd v2rayNG
git submodule update --init --recursive

# 3. 改图标 (可选): 替换 V2rayNG/app/src/main/res/mipmap-*/ic_launcher.png
#    启动页文案: V2rayNG/app/src/main/res/values/strings.xml
#    4. 推上去
git add . && git commit -m "feat: custom branding"
git push
# 5. Actions tab → Build APK → Run
```