# nvm 和 n
目前主流的node版本管理工具有两种，nvm和n。
两者差异挺大的，具体分析可以参考一下淘宝FED团队的一篇文章《管理 node 版本，选择 nvm 还是 n？》

总的来说，nvm有点类似于 Python 的 virtualenv 或者 Ruby 的 rvm，每个node版本的模块都会被安装在各自版本的沙箱里面（因此切换版本后模块需重新安装），因此考虑到需要时常对node版本进行切换测试兼容性和一些模块对node版本的限制，我选择了使用nvm作为管理工具，下面就来说说nvm的安装和使用过程。

# 安装流程

```javascript

curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.30.2/install.sh | bash

export NVM_DIR="$HOME/.nvm"

[ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh" # This loads nvm
```

