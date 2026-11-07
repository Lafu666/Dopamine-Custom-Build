# Dopamine Custom Build

只放「补丁 + 预装 deb + 构建流程」，不含 Dopamine 源码。每次构建实时拉取上游 `opa334/Dopamine` `3.x`，打补丁后编译出 `Dopamine.ipa`。

## 内容

| 路径 | 说明 |
|---|---|
| `patches/dopamine-3.x-custom.patch` | 三项改动的 git 补丁（13 文件，+633/-4） |
| `debs/*.deb` | 越狱时自动预装的 6 个包 |
| `.github/workflows/build-ipa.yml` | 构建流程 |

三项改动：首页长按背景自定义/恢复主题背景、首页显示版本更新时间与系统运行时间、越狱时自动预装 ellekit / preferenceloader / altlist / libsandy / choicy / trollstorelite。

## 出 IPA

仓库 **Actions** → `Build Dopamine IPA` → **Run workflow**（`mode` 选 `app-only`）→ 等绿 → 页面底部 **Artifacts** → 下载 `Dopamine-custom-ipa`，解压得 `Dopamine.ipa`。

`app-only` 只编译 App 本体，`basebin.tar` / `basebin.tc` / 内置 deb 取自上游客 3.0.13 IPA（本次改动未涉及 BaseBin 与 Packages，产物等价），约 5 分钟。需要从零全量编译就选 `full`，会装 Theos 编 BaseBin，约 30 分钟。

## 本地一键（把仓库建到你的账号下并取回 IPA）

```bash
GH_TOKEN=ghp_xxx python3 build_and_fetch.py --repo Dopamine-Custom-Build
```

脚本会建仓库、用 REST API 上传文件、触发 Actions、轮询、下载产物到 `/workspace/Dopamine-custom.ipa`。
