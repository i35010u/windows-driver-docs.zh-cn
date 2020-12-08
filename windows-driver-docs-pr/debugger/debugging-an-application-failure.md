---
title: 调试应用程序错误
description: 调试应用程序错误
keywords:
- 应用程序故障
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1a8df5e794ed869068a9948f63ccb86a377aa0f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817543"
---
# <a name="debugging-an-application-failure"></a>调试应用程序错误


## <span id="ddk_debugging_an_application_failure_dbg"></span><span id="DDK_DEBUGGING_AN_APPLICATION_FAILURE_DBG"></span>


用户模式应用程序中有多种可能的错误。

最常见的故障类型包括访问冲突、对齐错误、异常、临界区超时 (死锁) 和页面内 i/o 错误。

访问冲突和数据类型 misalignments 是最常见的。 如果取消引用无效的指针，通常会发生这种情况。 出现这种问题的原因可能是导致错误的函数或以前的函数向错误函数传递了无效参数。

用户模式异常有许多可能的原因。 如果发生未知异常，请在 ntstatus 或 winerror.h 中找到它（如果可能）。

关键部分超时 (或可能的死锁) 在一个线程长时间等待关键部分时发生。 它们难以调试，需要对堆栈跟踪进行深入分析。

页内 i/o 错误几乎总是硬件故障。 您可以通过仔细检查 ntstatus 中的状态代码来进行验证。

 

 





