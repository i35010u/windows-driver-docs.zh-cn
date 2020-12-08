---
title: Additive 模板指令
description: Additive 模板指令
keywords:
- 加法指令 WDK GDL
- 模板 WDK GDL，定义顺序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eefea9df77024686cce78496d1b6d4d6160617f5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794203"
---
# <a name="additive-template-directive"></a>Additive 模板指令


\***累加** 性：指令定义模板定义的顺序。

**加法** 指令可以具有以下值之一：

-   \_最近。 只显示最新的定义。

-   最 \_ 新的。 仅显示最早 (第一个) 定义。

-   最不 \_ 到最 \_ \_ 新。 所有定义按从最多到最新的顺序排列。

-   最起码 \_ 为 \_ 最 \_ 新。 所有定义的显示顺序从最小到最新。

如果此指令不存在，则假定默认值为 " \_ 最近"。

如果此指令本身在模板中定义或出现在多个通过继承关联的模板中，则只会接受最常使用的派生模板中最近定义的指令。

 

 




