---
title: 记录器限制和局限
description: 记录器限制和局限
ms.assetid: cb16c193-5420-4900-bf07-44b49859e296
keywords:
- 记录器限制
- 记录器限制
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1549e9ab32f9a156c454d92fe59319e0a1aeb3de
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519349"
---
# <a name="logger-restrictions-and-limitations"></a>记录器限制和局限


## <span id="ddk_logger_restrictions_and_limitations_dtoolq"></span><span id="DDK_LOGGER_RESTRICTIONS_AND_LIMITATIONS_DTOOLQ"></span>


记录器会增加堆栈消耗进程，因为它引入了另一个"包装"函数的实际函数调用之前。

这会暴露在通常与未初始化的变量相关的应用程序中的 bug。 记录器更改堆栈使用，因为函数调用中声明的本地变量可能不存在记录器比需要不同的初始值。 如果程序使用此变量，但不初始化，该程序可能会崩溃或否则的行为不同于记录器是否不存在。

遗憾的是，没有简单的方法解决此类问题。 唯一的解决方法是尝试在尝试隔离导致问题的区域中禁用函数的类别。

 

 





