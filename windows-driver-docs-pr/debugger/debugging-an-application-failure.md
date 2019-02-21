---
title: 调试应用程序故障
description: 调试应用程序故障
ms.assetid: c4118acb-2566-441a-8481-dee4bfdb03ba
keywords:
- 应用程序故障
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4fcf7d0401c12c06b8556f8d0e2b2048cf3aaefe
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545383"
---
# <a name="debugging-an-application-failure"></a>调试应用程序故障


## <span id="ddk_debugging_an_application_failure_dbg"></span><span id="DDK_DEBUGGING_AN_APPLICATION_FAILURE_DBG"></span>


有可能在用户模式应用程序中的各种错误。

最常见的失败类型包括访问冲突、 对齐错误、 异常、 关键部分超时值 （死锁） 和页 I/O 错误。

访问冲突和数据类型 misalignments 也是最常见。 它们通常会发生了无效的指针取消引用时。 使用导致此错误，该函数或使用了无效的参数传递给出错函数 earlier 函数可能位于意见。

用户模式异常都有许多可能的原因。 如果出现了未知的异常，可在可能的情况在 ntstatus.h 或 winerror.h 中找到。

当一个线程正在等待关键节很长时间时，会出现关键节超时 （或可能的死锁）。 这些是难以调试和需要的堆栈跟踪的深入分析。

在页 I/O 错误几乎始终是硬件故障。 您可以仔细检查 ntstatus.h 验证中的状态代码。

 

 





