# 如何避免使用sudo进行安装

使用 sudo 进行全局安装是一件让人很头疼的问题，特别是当你使 sudo 全局安装了 nbm cnpm 等包管理工具时，你以后使用 nbm cnpm 安装包时就都只能用 sudo 。
如果你也碰到过这些问题，是不是感觉整个世界都不友好了。
如何避免使用 sudo 进行全局安装呢，其实只要将你当前用户设置为 /user/local 的 owner 就可以了。
sudo chown -R $USER /usr/local
对于那些已经使用 sudo 安装过的包(eg: nbm cnpm)，一般在 /Users/{uer name}/.npm 文件夹下面，可以使用如下命令移除依赖 sudo。
sudo chown -R $USER /Users/$USER
这样你就可以和sudo说再见了。