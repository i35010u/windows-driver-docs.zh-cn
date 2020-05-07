---
title: Windows 内核模式内存管理器
description: Windows 内核模式内存管理器
ms.assetid: ab464d5b-7bad-494e-80cd-e32ca9e9fa8d
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 63b26330ec14e15c1fd536eeb1459e4953ac07d9
ms.sourcegitcommit: 6e2986506940c203a6a834a927a774b7efa6b86e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82800096"
---
# <a name="windows-kernel-mode-memory-manager"></a>Windows 内核模式内存管理器


Windows 内核模式内存管理器组件管理操作系统的物理内存。 此内存主要采用随机存取内存（RAM）的形式。

内存管理器通过执行以下主要任务来管理内存：

-   以虚拟和动态的方式管理内存的分配和释放。

-   支持内存映射文件、共享内存和写入时复制的概念。

有关驱动程序的内存管理的更多详细信息，请参阅[Windows 驱动程序的内存管理](managing-memory-for-drivers.md)。

向内存管理器提供直接接口的例程通常以字母 "**Mm**" 作为前缀;例如， **MmGetPhysicalAddress**。 若要查找有关内存管理器例程的文档，请导航到[**MmAdvanceMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmadvancemdl) ，并使用左侧的目录在 Mm * 例程中滚动。

有关按功能排序的内存管理器例程列表，请参阅[内存分配和缓冲区管理](https://docs.microsoft.com/windows-hardware/drivers/ddi/_kernel/#memory-allocation-and-buffer-management)。

 

 




