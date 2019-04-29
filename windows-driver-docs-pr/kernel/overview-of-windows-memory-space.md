---
title: Windows 内存空间概述
description: Windows 内存空间概述
ms.assetid: b49a35c2-6da6-4239-a67b-542d42a5c9e4
keywords:
- 内存管理 WDK 内核，有关内存空间
- 内存空间 WDK 内核
- 物理内存 WDK 内核
- 虚拟内存 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5773a3afab3cbd857cf86b25085b36de86b9f6f3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377931"
---
# <a name="overview-of-windows-memory-space"></a>Windows 内存空间概述





下图说明了基于 NT 的操作系统的虚拟内存空间和及其与系统物理内存。

![演示如何虚拟内存空间和物理内存的关系图](images/16vrtmem.gif)

如此图所示，虚拟内存由分页的物理内存，并可以由不连续的物理内存页来备份虚拟地址范围。 用户空间虚拟内存和分页池中分配的系统空间内存始终是*可分页*。 任何用户空间代码或数据可以出页到辅助存储在任何时候，即使正在执行进程。

请注意，任何非当前进程的虚拟地址是不可见，因此其内存空间是不可访问。

有关内存管理的全面介绍，请参阅*在 Microsoft Windows Internals* Microsoft press 书籍。

 

 




