---
title: Windows 内核模式内存管理器
description: Windows 内核模式内存管理器
ms.assetid: ab464d5b-7bad-494e-80cd-e32ca9e9fa8d
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: eb5728383445d9b803b8f12b05e8d7deba3082fc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358025"
---
# <a name="windows-kernel-mode-memory-manager"></a>Windows 内核模式内存管理器


Windows 内核模式内存管理器组件管理的操作系统的物理内存。 此内存是主要在随机存取内存 (RAM) 的形式。

内存管理器管理内存，通过执行以下主要任务：

-   几乎和动态管理分配和解除分配的内存。

-   支持内存映射文件、 共享的内存和写入时复制的概念。

详细了解驱动程序的内存管理的详细信息，请参阅[内存管理的 Windows 驱动程序](managing-memory-for-drivers.md)。

为内存管理器提供直接的界面的例程都通常带有前缀字母"**Mm**"; 例如， **MmGetPhysicalAddress**。 有关内存管理器例程的列表，请参阅[内存管理器例程](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554435(v=vs.85))。

有关内存管理器例程按功能列表，请参阅[内存分配数据和缓冲区管理](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_kernel/#memory-allocation-and-buffer-management)。

 

 




