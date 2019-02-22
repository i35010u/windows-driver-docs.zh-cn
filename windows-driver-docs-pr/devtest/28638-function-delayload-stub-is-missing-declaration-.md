---
title: C28638
description: 警告 C28638 函数延迟加载存根 （stub） 缺少匹配的声明。
ms.assetid: 25999552-6316-414b-972d-25797f477b15
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28638
ms.openlocfilehash: 1b52c49978388a95ed4daa2ad14aa3881f96229c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543737"
---
# <a name="c28638"></a>C28638


警告 C28638： 函数延迟加载存根 （stub） 缺少匹配的声明

可以不包括标头文件中的函数声明的情况下实现很多延迟加载存根 （stub）。 随着时间推移，函数签名可能会更改而不更新所有相应的延迟加载存根。 如果延迟加载存根 （stub） 有错误的签名，它会导致访问冲突。

通常情况下， **\#包括&lt;header.h&gt;**  ，其中包含的函数原型所实现的延迟加载存根是缺失。 一个常见错误是实现 （因此省略私有进程） 的公钥和私钥序号的延迟加载存根时包含公共头文件。 解决方法是延迟加载存根实现相应的标头文件包含在内。

 

 





