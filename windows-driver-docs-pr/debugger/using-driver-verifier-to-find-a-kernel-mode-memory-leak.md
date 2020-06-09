---
title: 使用驱动程序验证程序查找内核模式内存泄漏
description: 使用驱动程序验证程序查找内核模式内存泄漏
ms.assetid: d81a8b72-91d3-4132-9cc2-1cf1b597306a
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 954954781463b94081e1e0d468f31d6dd0f8802e
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534756"
---
# <a name="using-driver-verifier-to-find-a-kernel-mode-memory-leak"></a>使用驱动程序验证程序查找内核模式内存泄漏


驱动程序验证程序确定内核模式驱动程序是否正在泄漏内存。

驱动程序验证程序的池跟踪功能监视指定的驱动程序所执行的内存分配。 卸载驱动程序时，驱动程序验证程序会验证驱动程序所进行的所有分配是否已被释放。 如果未释放驱动程序的某些分配，则会发出 bug 检查，且 bug 检查的参数指示问题的性质。

此功能处于活动状态时，请使用驱动程序验证器管理器图形界面监视池分配统计信息。 如果将内核调试器附加到驱动程序，请使用[**！ verifier 0x3**](-verifier.md)扩展显示分配统计信息。

如果驱动程序使用直接内存访问（DMA），则驱动程序验证程序的 DMA 验证功能对于查找内存泄漏也很有用。 DMA 验证测试了许多常见的误用了 DMA 例程，包括无法释放常见缓冲区和可能导致内存泄漏的其他错误。 如果在此选项处于活动状态时连接内核调试器，请使用[**！ dma**](-dma.md)扩展显示分配统计信息。

有关驱动程序验证程序的信息，请参阅 Windows 驱动程序工具包（WDK）文档中的[驱动程序验证程序](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)。

 

 





