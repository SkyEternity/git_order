

```
# gitlab 里面需要fork一个地址
# 假设上游仓库的地址是 git@192.168.57.74/baodan/agent.git
# 假设当前用户gitlab用户名为example，那么fork后的仓库地址应该是 git@192.168.57.74/example/agent.git
# clone上游仓库到本地（已经clone过可跳过此步骤）
git clone git@192.168.57.74/baodan/agent.git

# 配置自己Fork的仓库地址（假设以前没有配置过）
git remote add example git@192.168.57.74/example/agent.git
# 查看fork 地址
git remote -v
# 删掉其中的fork 
git remote rm name
# 给fork 重新定义url
git remote set-url origin 链接

# 同步代码
git checkout master
git pull origin master

# 创建特性分支branch
git checkout origin/master -b 'branch'


# 开发新特性...
# 提交代码
git add .
# 提交到本地版本库
git commit -m 'your commit message'
# 推送到自己Fork的仓库
git push example branch
# 打开gitlab页面创建Merge Request
```

代码审查过程中的问题可以直接在Gitlab的Merge Request页面评论，这样相关人员能收到邮件通知。

开发者要定期更新自己仓库的Master分支来保证与上游仓库（即：你Fork的那个仓库）的代码保持同步， 这样可以减小Merge Request中代码冲突的概率。

如果Merge Request中存在代码冲突，应该由提交Merge Request的人负责解决冲突后重新push一次代码（无需重建Merge Request）。

另外，为保证Pull Request的整洁，尽量在Merge之前合并一下提交，具体参考如下命令：

```
# 同步主分支
git fetch origin master

# 合并分支
# 修改要合并的pick为s 然后wq 退出
git rebase -i origin/master
合并完后 需要提交代码到该分支 git push example branch -f

#查看分支
git branch
#删除分支 
git branch -D 'name'

#冲突
git fetch origin master
git rebase -i origin master
#若是有冲突 先解决冲突
 git add .
 git rebase --continue
```

[** Clone repository](https://gitlab.com/funxdata/forum/wikis/git_access)[Home](https://gitlab.com/funxdata/forum/wikis/home)[团队协作规范](https://gitlab.com/funxdata/forum/wikis/%E5%9B%A2%E9%98%9F%E5%8D%8F%E4%BD%9C%E8%A7%84%E8%8C%83)[微服务架构带来的变化](https://gitlab.com/funxdata/forum/wikis/%E5%BE%AE%E6%9C%8D%E5%8A%A1%E6%9E%B6%E6%9E%84%E5%B8%A6%E6%9D%A5%E7%9A%84%E5%8F%98%E5%8C%96)[服务化架构流程及开发](https://gitlab.com/funxdata/forum/wikis/%E6%9C%8D%E5%8A%A1%E5%8C%96%E6%9E%B6%E6%9E%84%E6%B5%81%E7%A8%8B%E5%8F%8A%E5%BC%80%E5%8F%91)
