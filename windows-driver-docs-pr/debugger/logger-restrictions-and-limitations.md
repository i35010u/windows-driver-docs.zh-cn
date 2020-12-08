---
title: 记录器的局限性和限制
description: 记录器的局限性和限制
keywords:
- 记录器，限制
- 记录器，限制
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6b551b146ca9309609454298f8f88539b6bccbf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819165"
---
# <a name="logger-restrictions-and-limitations"></a>记录器的局限性和限制


## <span id="ddk_logger_restrictions_and_limitations_dtoolq"></span><span id="DDK_LOGGER_RESTRICTIONS_AND_LIMITATIONS_DTOOLQ"></span>


记录器会增加进程的堆栈消耗，因为它会在实际函数调用之前引入额外的 "包装" 函数。

这可能会在通常与未初始化的变量相关的应用程序中公开 bug。 由于记录器会改变堆栈的使用，因此，在函数调用中声明的局部变量可能会采用不同于不存在记录器的初始值。 如果程序在不初始化的情况下使用此变量，则该程序可能会崩溃，或与记录器不存在时的行为方式不同。

遗憾的是，没有一种简单的方法可解决这种问题。 唯一的解决方法是尝试禁用函数类别，尝试隔离导致问题的区域。

 

 





