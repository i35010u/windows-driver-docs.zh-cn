---
title: 在 KMDF 驱动程序中处理 DMA 操作
description: 介绍如何 KMDF 驱动程序将 I/O 请求转换为直接内存访问 (DMA) 的操作。 KMDF 支持总线 master 和系统模式 DMA。
ms.assetid: 1ca8ba66-201d-42f2-a6f1-6184a9d7c2a6
keywords:
- 内核模式驱动程序 WDK KMDF，DMA 操作
- KMDF WDK，DMA 操作
- 内核模式驱动程序框架 WDK，DMA 操作
- 基于框架的驱动程序 WDK KMDF，DMA 操作
- DMA 操作 WDK KMDF
- 主总线 DMA WDK KMDF
- 直接内存访问 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f2d6e0e64977d32f4af41eaf9024affdae2c8dac
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382852"
---
# <a name="handling-dma-operations-in-kmdf-drivers"></a>在 KMDF 驱动程序中处理 DMA 操作


\[仅适用于 KMDF\]

本部分介绍如何内核模式驱动程序框架 (KMDF) 驱动程序将 I/O 请求转换为直接内存访问 (DMA) 的操作。 KMDF 支持总线 master 和系统模式 DMA。




## <a name="in-this-section"></a>本节内容


-   [在 Windows 驱动程序框架的 DMA 简介](introduction-to-dma-in-windows-driver-framework.md)
-   [Framework DMA 对象](framework-dma-objects.md)
-   [DMA 事务和 DMA 传输](dma-transactions-and-dma-transfers.md)
-   [使用框架 DMA 的示例驱动程序](sample-drivers-that-use-framework-dma.md)
-   [主总线 DMA 设备 KMDF 驱动程序中处理 I/O 请求](handling-i-o-requests-in-a-kmdf-driver-for-a-bus-master-dma-device.md)
-   [支持系统模式 DMA](supporting-system-mode-dma.md)
-   [正在取消 DMA 事务](canceling-dma-transactions.md)
-   [保留 DMA 资源](reserving-dma-resources.md)
-   [DMA 测试 KMDF 驱动程序中](testing-dma-in-kmdf-drivers.md)

了解如何在 WDM 驱动程序支持 DMA 操作，请参阅[DMA 编程技术](https://docs.microsoft.com/windows-hardware/drivers/kernel/dma-programming-techniques)。

 

 





