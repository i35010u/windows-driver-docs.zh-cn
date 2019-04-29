---
title: 使用驱动程序验证程序查找内核模式内存泄漏
description: 使用驱动程序验证程序查找内核模式内存泄漏
ms.assetid: d81a8b72-91d3-4132-9cc2-1cf1b597306a
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c34d767fe386a3c1982bc6bea1cb0e80a37b18b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378475"
---
# <a name="using-driver-verifier-to-find-a-kernel-mode-memory-leak"></a>使用驱动程序验证程序查找内核模式内存泄漏


驱动程序验证程序确定的内核模式驱动程序是否正在泄漏内存。

驱动程序验证程序的池跟踪功能监视由指定的驱动程序进行的内存分配。 在驱动程序被卸载时，驱动程序验证程序验证已释放的驱动程序所做的所有分配。 如果尚未释放一些驱动程序的分配，发出的 bug 检查，并检查错误的参数指示问题的性质。

虽然此功能处于活动状态，使用驱动程序验证程序管理器图形界面来监视池分配统计信息。 如果内核调试程序附加到该驱动程序，使用[ **！ verifier 0x3** ](-verifier.md)扩展以显示分配统计信息。

如果驱动程序使用直接内存访问 (DMA)，DMA 验证功能的驱动程序验证程序也是很有帮助中查找内存泄漏。 DMA 验证测试多个常见 DMA 例程，包括故障免费常见缓冲区和其他错误，可能会导致内存泄漏的误用。 如果内核调试器已附加此选项处于活动状态时，使用[ **！ dma** ](-dma.md)扩展才会显示分配的统计信息。

有关驱动程序验证程序的信息，请参阅[Driver Verifier](https://go.microsoft.com/fwlink/p/?linkid=120480) Windows Driver Kit (WDK) 文档中。

 

 





