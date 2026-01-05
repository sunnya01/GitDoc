Git总结

1. 常用命令: git config –global user.name or email or password “value”,不带“value”表示查询，带了“value”表示用value的更改值
2. Git -branch 查询本地分支 git -branch -r 查看远程分支
3. 克隆远程库-http版本，cd到指定目录 git clone “远端地址”
4. 提交到远端库-http版本，cd 到远端库的本地文件中，然后git add 修改过的文件名
5. Git commit -m “修改原因”，添加远端地址 git remote add origin “远端地址”
6. Git push -u origin master
7. 然后会提示输入账号密码。(tips:如果对同一个产品例如github推送远端库并且切换了账号会遇到403的问题，windows通过win+凭据管理器->windows凭据->普通凭据搜索github删除旧的验证信息，mac->command+shift+g搜索路径/System/Library/CoreServices/Applications/->找到钥匙管理器。搜索github删除对应记录)
8. ssh版本 首先本地生成ssh密钥，ssh-keygen -t rsa -C “email“ -> 输入文件名称默认id_rsa ->输入访问ssh密钥的密码 -> vi 密钥文件.pub 拷贝里面的内容 然后去github-setting下面新增ssh密钥，如果存在多个密钥
9. 需要touch config在~/.ssh目录下面新增config文件无后缀名
10. 里面的内容填写例
11. /# GitHub (#表示注释)
12. Host github.com
    HostName github.com
    PreferredAuthentications publickey
    IdentityFile ~/.ssh/github_id_rsa
13. 克隆远程库-ssh版本，cd到指定目录git clone “远端地址”
14. 提交到到远端
15. git 常用命令 git add filename.后缀 git commmit -m "修改原因" git push -u origin master git remote  ctrl + z 退出 
16. 添加远端 git remote add remote <远程仓库的URL>