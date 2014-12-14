# download source
由于 SDK 比较大，请选择以下云盘之一下载 firefly-rk3288_sdk_git_20141211.tar.gz ：


# 下载完成后先验证一下 MD5 码：
    $ md5sum /path/to/firefly-rk3288_sdk_git_20141211.tar.gz
     8fe99f519d487ff40c8bc7b5ded62887  firefly-rk3288_sdk_git_20141211.tar.gz

 确认无误后，就可以解压：

    mkdir -p ~/proj/firefly-rk3288
    cd ~/proj/firefly-rk3288
    tar xf /path/to/firefly-rk3288_sdk_git_20141211.tar.gz
    git reset --hard
    git remote add bitbucket https://bitbucket.org/T-Firefly/firefly-rk3288.git

#  以后就可以直接从 bitbucket 处更新：

    git pull bitbucket master:master

