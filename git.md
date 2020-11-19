# git

想要让git对一个目录进行版本控制需要一下步骤：

* 进入要管理的文件夹

* 执行初始化名利

    ```
    git init
    ```

* 查看管理目录下的文件状态

    ```
    git status
    
    新增的文件和修改后的文件都是红色的（未管理的）
    ```

* 管理指定文件（红变绿）

    ```
    git add 文件名
    git .
    git *
    ```

* 个人信息配置

    ```
    git config --global user.email ""
    git config --global user.name ""
    ```

* 生成版本

    ```
    git commit -m '版本信息'
    ```

* 查看版本记录

    ```
    git log
    ```

* 回滚至之前版本

    ```
    git log 查看版本信息  hash值
    git reset --hard  版本号(版本hash值)
    ```

* 回滚至回滚之后的版本

    ```
    git reflog
    git reset --hard 版本号
    ```

* 取消修改

    ```
    git checkout -- 文件名
    ```

* 查看分支

    ```
    git branch
    ```

* 创建分支

    ```
    git branch 分支总称
    git checkout -b 分支名   创建分支并切换到分支
    ```

* 切换分支

    ```
    git checkout 分支名称
    ```

* 分支合并(可能产生冲突)

    ```
    git merge 要合并的分支名称
    
    注意：切换分支再合并
    ```

* 删除分支

    ```
    git branch -d 删除的分支名
    ```

* 给远程仓库起别名

    ```
    git remote add origin https://github.com/cy77cc/learngit.git
    ```

* 提交代码到github

    ```
    git push -u origin 分支名称
    ```

* 拉取代码

    ```
    git clone 远程仓库的地址   仅一次
    ```

* 拉取代码

    ```
    git pull origin 分支名
    等价于
    git fetch origin 分支名
    git merge origin/分支名
    ```

* git rebase使用

    ```
    git rebase -i 版本hash值(从上到下合并到对应的版本) 或  HEAD~合并条数
    ```


![image-20201105190752620](C:\Users\48356\Desktop\笔记\image\image-20201105190752620.png)

* 情况1 解决版本过多

    ```
    git rebase -i HEAD~3
    ```

* 情况2  解决分叉

    ```
    git checkout dev
    git rebase master
    git checkout master
    git merge dev
    ```

* 情况3 解决冲突

    ```
    git checkout dev
    git rebase master  会提示冲突报错
    解决冲突问题之后
    git rebase --continue
    ```

* 记录图形化显示

    ```
    git log --graph --pretty=format:"%h %s"
    ```

* 给版本起tag

    ```
    git tag -a 标签名 -m "描述"
    ```

* 更新远程仓库版本

    ```
    git push origin --tags
    ```

* 运营下载代码

    ```
    git clone -b 版本号 地址
    ```

* git忽略文件

    ```
    .gitignore
    ```

    
