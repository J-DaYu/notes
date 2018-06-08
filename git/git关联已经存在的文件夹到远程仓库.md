# git关联已经存在的文件夹到远程仓库

> 本地已经存在项目代码, 此时需要关联远端仓库

```bash
cd path/to/project
git init
# repositoryname 如果远程仓库不存在则会创建一个名称为 repositoryname 的仓库 (gitlab)
git remote add origin git@host:user/repositoryname.git
git add .
git commit -m "Initial commit"
git push -u origin master
```

