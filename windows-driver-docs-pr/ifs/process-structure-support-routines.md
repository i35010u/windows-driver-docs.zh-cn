---
title: 进程结构支持例程
description: 进程结构支持例程
ms.assetid: 2cf3ab25-9db8-4a20-982d-eda0c3c96dbc
ms.date: 09/30/2019
ms.localizationpriority: medium
ms.openlocfilehash: ebc1def03cc42ee5f59a618556053e0fdc8a7ae0
ms.sourcegitcommit: c23a403b3ebea05bde96067b678a318ca9b0cabe
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2019
ms.locfileid: "71955825"
---
# <a name="process-structure-support-routines"></a>进程结构支持例程

下表列出了系统提供的进程结构支持例程的子集，这些例程可由内核模式文件系统和微筛选器和旧筛选器驱动程序使用。 设备驱动程序无法使用这些例程。

除了此处所述的例程，文件系统和筛选器驱动程序还可以调用内核模式驱动程序体系结构参考部分中所述的任何**Ps**_Xxx_例程，并在*ntifs*中声明。

**头文件：** *ntifs*

**Prefix：Ps @ no__t-0_Xxx_

| 函数或宏 | 描述 |
| ----------------- | ----------- |
| **PsChargePoolQuota** | 指定进程的指定池类型的费用池配额。 |
| **PsDereferenceImpersonationToken** | 递减模拟标记的引用计数。 |
| **PsDereferencePrimaryToken** | 递减主令牌的引用计数。 |
| **PsIsDiskCountersEnabled** | 返回每个进程磁盘 i/o 计数器的启用状态。 |
| **PsGetProcessExitTime** | 返回当前进程的退出时间。 |
| **PsImpersonateClient** | 使服务器线程模拟客户端。 |
| **PsIsThreadTerminating** | 检查线程是否正在终止。 |
| **PsLookupProcessByProcessId** | 接受进程的进程 ID 并返回指向进程的 EPROCESS 结构的引用指针。 |
| **PsLookupThreadByThreadId** | 接受线程的线程 ID 并返回指向该线程的 ETHREAD 结构的引用指针。 |
| **PsReferenceImpersonationToken** | 递增指定线程的模拟标记的引用计数。 |
| **PsReferencePrimaryToken** | 递增指定进程的主标记的引用计数。 |
| **PsReturnPoolQuota** | 将指定池类型的池配额返回到指定进程。 |
| **PsRevertToSelf** | 结束调用方的客户端模拟。 |
| **PsUpdateDiskCounters** | 更新给定进程的磁盘 i/o 计数器。 |
