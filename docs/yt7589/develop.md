# DeepSeekTUI开发手册

# 附录A. 源码安装
首先要在系统中安装Rust开发环境，接下来安装步骤：
配置Rust源
```bash
vim ~/.cargo/config.toml
##############################################################################################
[source.crates-io]
replace-with = "tuna"

[source.tuna]
registry = "sparse+https://mirrors.tuna.tsinghua.edu.cn/crates.io-index/"
##############################################################################################
```

编译源码
```bash
# Linux build deps (Debian/Ubuntu/RHEL):
sudo apt-get install -y build-essential pkg-config libdbus-1-dev
sudo dnf install -y gcc make pkgconf libdbus-1-dev

git clone https://github.com/Hmbown/DeepSeek-TUI.git
cd DeepSeek-TUI

cargo install --path crates/cli --locked   # requires Rust 1.88+; provides `deepseek`
cargo install --path crates/tui --locked   # provides `deepseek-tui`
```

基本使用
```bash
deepseek auth set --provider deepseek # 会提示输入DeepSeek密钥，并保存到~/.deepseek/config.toml
deepseek auth status
```

贡献源码方式
```bash
# Fork源项目为：https://github.com/yt7589/DeepSeek-TUI
# 查看当前远程仓库（应该只有 origin，指向原项目）
git remote -v
# 添加你自己的 Fork 仓库作为新的远程仓库（通常叫 myfork）
git remote add yt7589DeepSeekTui https://github.com/yt7589/DeepSeek-TUI.git

# 设置公钥访问
# 1. 生成 SSH 密钥（如果还没有）
ssh-keygen -t ed25519 -C "yt7589@qq.com"
# 2. 查看并复制公钥
cat ~/.ssh/id_ed25519.pub
# 3. 登录 GitHub → Settings → SSH and GPG keys → New SSH key，粘贴公钥
# 4. 修改远程仓库 URL 为 SSH 格式
git remote set-url yt7589DeepSeekTui git@github.com:yt7589/DeepSeek-TUI.git
# 5. 测试连接
ssh -T git@github.com

# 将改动提交到自己的源码库中
git checkout -b yt7589dev
git add .
git commit -m "..."
git push -u yt7589DeepSeekTui yt7589dev

# 贡献自己的代码
```