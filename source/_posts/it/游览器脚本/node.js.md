
# npm 
## npm cache
> NPM会把所有下载的包保存，放在用户文件夹下面 关联package.lock.json的sha1值保存
## npm cache verify
> 确保所有内容一致
## npm cache clean -—force
> 删除所有缓存文件
npm install --cache /tmp/empty-cache
> 使用临时缓存调试安装程序的问题