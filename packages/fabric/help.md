#fabric 使用帮助文档
```
通过该文档,能够学会使用fabric 的基本命令,并使用命令去部署服务器
```
##DEMO
```python
# fabfiles.py
# 导入fabric API中的一些模块,run 主要是在服务器执行参数中的部署命令;local 是在本地执行相应
# 的命令;setting接受一个或多个键/值对参数，用于修改其代码块内部的 env; env 主要配置一些与环境相关的
# 变量值,比如host 主机名称,user 用户,password 密码。
from fabric.api import run, setting, local, env
#  主机地址列表,可以同时指定多个主机的地址
env.host = ['8.8.8.8',]
# 所有主机的用户名, 进一步可以通过对主机进行分组,配置不同的用户信息
env.user = 'root'
# 所有主机指定用户名的密码
env.password = ''

# 编写一个函数判断指定路径是否存在文件或文件夹
def exists(path):
    with setting(warn_only=True):
        run('([ -f "%s" ] || [ -d '%s' ]) && echo 0 || echo 1' % path)

```
```shell
# 使用fab命令执行fabfiles 中的 exists 函数.
fab -f fabfiles.py exists:path='dir'
```
