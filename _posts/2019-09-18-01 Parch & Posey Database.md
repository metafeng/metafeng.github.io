---
layout: post
title: "「SQL For Data Analysis」01 Parch & Posey Database"
subtitle: '用 Parch & Posey 的数据来回答问题'
author: "Hufe"
header-img: "img/post-bg-mysql.jpg"
header-mask: 0.3
tags:
  - SQL For Data Analysis
  - SQL
---

# Parch & Posey Database

本案例的数据来自 Parch & Posey, 这家公司的业务是销售纸张，他们有 50 位销售代表，遍布美国四大地区，他们销售的纸张有三种：普通纸、海报纸和高光铜版纸（regular, poster, and glossy），客户主要是财富 100 强的大企业，这些客户主要是由 Google、 Facebook 和 Twitter 上的广告招商过来的。

Parch & Posey 并不是个真实的公司，是我们捏造的 所有数据也是假的 只是为了本次案例。

数据集下载 [github/parch_posey_origin_dataset](<https://github.com/hufe09/parch_posey_origin_dataset>)

*structure_parch_posey.sql* 为数据库结构。其他文件为各个数据表数据。

你将用 Parch & Posey 的数据来回答问题，这些问题是参照现实问题而设的，使用 SQL 我们能帮 Parch & Posey 回答一些棘手的难题 如：1. 哪条产品线业绩最差？2. 该往哪个营销渠道追加更多投资？

## 1. 实体关系图

实体关系图 (ERD, Entity Relationship Diagram) 是查看数据库中数据的常用方式。下面是我们将用于 Parch & Posey 数据库的 ERD。这些图可帮助你可视化正在分析的数据，包括:

- 表的名称。 
- 每个表中的列。 
- 表配合工作的方式。

你可以将下面的每个框看作一个电子表格。

![Parch_Posey ERD](https://gitee.com/hufe09/image_hosting/raw/master/PicGo/Parch_Posey.png)

![title](https://gitee.com/hufe09/image_hosting/raw/master/PicGo/NtaeC1mzfAdJBjW.png)


注意事项
在 Parch & Posey 数据库中，共有五个表（基本上是 5 个电子表格）: 

- web_events 
- accounts 
- orders 
- sales_reps 
- region 

![title](https://gitee.com/hufe09/image_hosting/raw/master/PicGo/Z1LaTqj9SMBpU4l.png)

你可以将每个表视为一个单独的电子表格。然后将每个电子表格中的列放在表名下面。例如，**region** 表有两列: id 和 name，而 **web_events** 表有四列。

## 2. 为什么企业喜欢使用数据库

**1.**   只有输入了需要输入的数据，以及只有某些用户能够将数据输入数据库，才能**保证数据的完整性**。

**2.**    **可以快速访问数据** - SQL 可使我们从数据库中快速获取结果。 可以优化代码，快速获取结果。 

**3.**    **可以很容易共享数据** - 多个人可以访问存储在数据库中的数据，所有访问数据库的用户获得的数据都是一样。

 

## 3. 关于 SQL 数据库中所存储数据的几个要点

**1.**    **数据库中的数据存储在类似于** **Excel** **电子表格的表中。** 大多数情况下，可以将数据库视为一堆 Excel 电子表格。每个电子表格都有行和列。每行保存有关交易、个人、公司等的数据。而每列所保存的数据与你关心的某一特定行相关，如名称、位置、唯一身份等。

**2.**    **同一列中的所有数据必须符合数据类型。** 将整个列认为是定量离散的或是某种字符串。这说明如果特定列中有一行字符串，那么整个列可能会更改为文本数据类型。 **如果想使用此列进行数学计算，这可能会非常糟糕！** 

**3.**    **列类型一致是快速使用数据库的主要原因之一**。 
 数据库通常会存储**海量**数据。因此，知道这些列都是相同类型的数据意味着可快速从数据库获取数据。



## 4. 入门 SQL 并不难

SQL 功能这么强大，那么学起来会很难吗？一点也不。SQL 不需要像其他语言那样，学习起来需要大量的程序语言基础，SQL 更像是一门英语，有一些简单的英语单词，当你使用它的时候，就好像在用英语与数据库进行对话。

我们可以把 SQL 语言按照功能划分成以下的 4 个部分：

1. DDL，英文叫做 Data Definition Language，也就是数据定义语言，它用来定义我们的数据库对象，包括数据库、数据表和列。通过使用 DDL，我们可以创建，删除和修改数据库和表结构。
2. DML，英文叫做 Data Manipulation Language，数据操作语言，我们用它操作和数据库相关的记录，比如增加、删除、修改数据表中的记录。
3. DCL，英文叫做 Data Control Language，数据控制语言，我们用它来定义访问权限和安全级别。
4. DQL，英文叫做 Data Query Language，数据查询语言，我们用它查询想要的记录，它是 SQL 语言的重中之重。在实际的业务中，我们绝大多数情况下都是在和查询打交道，因此学会编写正确且高效的查询语句，是学习的重点。