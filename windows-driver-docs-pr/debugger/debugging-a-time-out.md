---
title: 调试超时
description: 调试超时
ms.assetid: 795774da-10fb-4431-908d-94c3baa01132
keywords:
- 超时
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52aa4d073c745b40201cbc064fc3c71b0d00f142
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324597"
---
# <a name="debugging-a-time-out"></a>调试超时


## <span id="ddk_debugging_time_outs_dbg"></span><span id="DDK_DEBUGGING_TIME_OUTS_DBG"></span>


有两个主要超时发生在 Windows 系统上：

[资源超时](resource-time-outs.md)（内核模式）

[关键部分超时](critical-section-time-outs.md)（用户模式）

在许多情况下，这些问题是线程的只需花费太长，无法发布资源或退出代码部分。

在零售系统中，超时值设置得足够高，则不会看到 （将只挂起，则返回 true 的死锁） 的中断。 在注册表中设置的超时值**HKEY\_本地\_机\\系统\\CurrentControlSet\\控制\\SessionManager**。 整数值在每个超时中指定秒的数。

 

 





