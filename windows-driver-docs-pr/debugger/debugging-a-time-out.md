---
title: 调试超时
description: 调试超时
keywords:
- 超时
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a34171e1a39f22ac80b0e891914128c614848a9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838233"
---
# <a name="debugging-a-time-out"></a>调试超时


## <span id="ddk_debugging_time_outs_dbg"></span><span id="DDK_DEBUGGING_TIME_OUTS_DBG"></span>


Windows 系统上发生了两个主要的时间：

 (内核模式) 的[资源超时](resource-time-outs.md)

[临界区超时](critical-section-time-outs.md) (用户模式) 

在许多情况下，这些问题只是一个线程释放资源或退出代码段所需的时间太长。

在零售系统上，超时值设置得足够高，以致于真正的死锁 (会导致) 中断。 在注册表中的 **HKEY \_ LOCAL \_ MACHINE \\ System \\ CurrentControlSet \\ Control \\ SessionManager** 下设置超时值。 整数值指定每个超时中的秒数。

 

 





