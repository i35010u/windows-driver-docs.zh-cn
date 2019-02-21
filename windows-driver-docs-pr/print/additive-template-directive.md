---
title: 累加性模板指令
description: 累加性模板指令
ms.assetid: 94883a51-a3a6-492e-9597-6a2f913d40bc
keywords:
- 累加性指令 WDK GDL
- 模板 WDK GDL，定义的顺序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78b313c5588761c01a6db6cef331ccb445236dcf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554467"
---
# <a name="additive-template-directive"></a>累加性模板指令


\***累加性**： 指令定义的模板定义的顺序。

**累加性**指令可以具有以下值之一：

-   大多数\_最近。 仅最新的定义将显示。

-   最低\_最近。 将显示的最早 (first) 定义。

-   大多数\_TO\_最低\_最近。 所有定义都显示从最到最有序。

-   最低\_TO\_大多数\_最近。 所有定义都显示顺序从最低到最新。

如果此指令不存在，默认值为大多数\_最近将假定。

如果此指令本身多次的模板中定义，或者将显示在通过继承相关的多个模板，将遵循派生程度最高的模板中仅最新定义的指令。

 

 




