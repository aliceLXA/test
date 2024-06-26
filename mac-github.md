master套卡片
1111
配置 macOS 上的 SSH keys 用于 GitHub 的步骤如下：

# 生成 SSH Key：

 打开“终端”应用程序，然后输入以下命令：
```ssh-config
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```
 这将在 ~/.ssh/ 目录下生成一个新的 SSH key。

# 添加 SSH Key 到 ssh-agent：

 首先，确保 ssh-agent 在后台运行：
 
```ssh-config
eval "$(ssh-agent -s)"
```
 然后添加 SSH private key 到 ssh-agent：

```ssh-config
ssh-add -K ~/.ssh/id_rsa
```
将 SSH Key 添加到 GitHub：

# 复制 SSH key 到剪贴板：
```ssh-config
pbcopy < ~/.ssh/id_rsa.pub
```
登录到你的 GitHub 账户，进入 “设置（Settings）” -> “SSH 和 GPG 密钥（SSH and GPG keys）”。

点击 “新建 SSH 密钥（New SSH key）”，然后粘贴你复制的公钥。

# 测试连接：

 在终端中输入以下命令：

```ssh-config
ssh -T git@github.com
```
 如果一切设置正确，你应该会看到一条消息，说你已经成功地认证了。

现在，当你从 GitHub 克隆或推送代码时，会使用这个 SSH key。这样，你就不需要每次都输入用户名和密码了。


# 如果报错"Host key verification failed."
你可以手动使用 ssh-keygen 命令来验证远程服务器的 host key。例如，对于 GitHub，你可以运行：
```ssh-config
ssh-keyscan -t rsa github.com >> ~/.ssh/known_hosts
```