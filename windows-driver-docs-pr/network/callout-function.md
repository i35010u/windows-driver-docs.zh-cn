---
title: 标注函数
description: 标注函数
ms.assetid: cf7b8e69-e6b2-41ac-9906-f0e3c090eb7a
keywords:
- 标注函数 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 596e4e19fafe9952299a6cce5f4d6273d5afb3a6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526210"
---
# <a name="callout-function"></a>标注函数


一个*标注函数*是一个函数，由实现[标注驱动程序](callout-driver.md)，它是定义的函数之一[标注](callout.md)。 下面的标注函数列表包含一个标注：

-   一个[ *notifyFn* ](https://msdn.microsoft.com/library/windows/hardware/ff568803)函数来处理通知。

-   一个[ *classifyFn* ](https://msdn.microsoft.com/library/windows/hardware/ff544890)进程分类的函数。

-   一个[ *flowDeleteFn* ](https://msdn.microsoft.com/library/windows/hardware/ff550025)过程流删除操作 （可选） 的函数。

[筛选器引擎](filter-engine.md)标注的标注函数以便标注可以处理的网络数据的调用。

 

 





