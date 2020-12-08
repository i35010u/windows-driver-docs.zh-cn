---
title: C28638
description: 警告 C28638 函数延迟加载存根缺少匹配的声明。
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28638
ms.openlocfilehash: f560652d7568b81876b986b68d8fbce053cb928e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819805"
---
# <a name="c28638"></a>C28638


警告 C28638：函数延迟加载存根缺少匹配的声明

许多延迟-加载存根可以实现，而无需包含声明函数的头文件。 随着时间的推移，函数签名可能会更改，而不会更新所有对应的延迟加载存根。 如果延迟加载存根具有错误的签名，则会导致访问冲突。

通常，包含所实现的延迟加载存根的函数原型的 **\# include &lt; 标头为 &gt; 。** 常见的错误是在为公共和专用序号实现延迟加载存根时包含公共头文件， (因此将省略专用序号) 。 解决方法是为所实现的延迟加载存根包括适当的标头文件。

 

 





