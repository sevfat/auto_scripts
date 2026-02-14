# auto_weirdhost  kr的ck登录续期


你需要做以下修改：


## 1、设置环境变量，环境变量格式如下：

- PRIVATE_REPO_TOKEN （用于读取私库的 token，可跟其他库共用）

- WEIRDHOST_REMEMBER_WEB_COOKIE

- WEIRDHOST_TG_BOT_TOKEN  (可选)
- WEIRDHOST_TG_CHAT_ID     (可选)



## 2、开放自动写time.txt的文件权限。
### 这个主要是用于规避github 默认60天的仓库代码没有任何变动就会自动给你发邮件并且自动禁用action的定时任务。

GITHUB_TOKEN 不用你手动创建 —— 只要你的 workflow 在 GitHub Actions 里跑起来，GitHub 会自动为每次运行生成一个临时的 secrets.GITHUB_TOKEN，在 workflow 里直接用就行（你已经在用 ${{ secrets.GITHUB_TOKEN }} 了）。

### 你需要做的通常是 给它权限、以及确认 checkout 会把它用在 push 上。

1) 你不需要创建：它默认就存在,在 workflow 里这样写就能用：
```
env:
  GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}

```

这个 secrets.GITHUB_TOKEN 是 GitHub 自动注入的，不会出现在 “Secrets” 列表里让你手动建。


2) 你需要设置的地方：给它写权限

到仓库：

### Settings → Actions → General → Workflow permissions

选择：

✅ Read and write permissions



## 3、修改定时任务执行时间。
### weirdhost-AutoRenew.yml里面修改你的定时任务的执行时间


