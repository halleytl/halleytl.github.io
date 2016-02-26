---
layout: post
title: "Git 需要一点点记 "
description: ""
category: 
theme: 
  name: "bootstrap-3"
tags: [Git]
---
{% include JB/setup %}


1. 显示文件的每一行是在那个版本最后修改

```shell
git blame filename
```

2. 显示某个文件的每个版本提交信息：提交日期，提交人员，版本号，提交备注（没有修改细节）

```shell
git whatchanged 5aa1be6674ecf6c36a579521708bf6e5efb6795f
```

3. 显示某个版本的修改详情

```shell
git show 5aa1be6674ecf6c36a579521708bf6e5efb6795f
```

4. 显示某个版本的某个文件修改情况

```shell
git show 5aa1be6674ecf6c36a579521708bf6e5efb6795f filename
```







