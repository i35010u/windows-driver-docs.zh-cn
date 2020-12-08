---
title: Windows 内存空间概述
description: Windows 内存空间概述
keywords:
- 内存管理 WDK 内核，关于内存空间
- 内存空间 WDK 内核
- 物理内存 WDK 内核
- 虚拟内存 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 517ee46c4d17579dc79bf5c3fd4122d28f541cf3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837219"
---
# <a name="overview-of-windows-memory-space"></a>Windows 内存空间概述





下图说明了基于 NT 的操作系统的虚拟内存空间及其与系统物理内存的关系。

![阐释虚拟内存空间和物理内存的示意图](images/16vrtmem.gif)

如图所示，虚拟内存由分页的物理内存支持，而不连续的物理内存页可以支持虚拟地址范围。 从分页池分配的用户空间虚拟内存和系统空间内存始终是可 *分页* 的。 即使在执行进程时，任何用户空间代码或数据都可以随时分页到辅助存储。

请注意，任何非当前进程的虚拟地址都不可见，因此无法访问其内存空间。

有关内存管理的详细讨论，请参阅 Microsoft 新闻中的 *Microsoft Windows* 内部内容手册。

 

 




