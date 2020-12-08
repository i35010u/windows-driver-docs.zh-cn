---
title: 在 KMDF 驱动程序中测试 DMA
description: 在 KMDF 驱动程序中测试 DMA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4eac3ce3cfc3ce27e5bf271a307a3d218ff6328b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836563"
---
# <a name="testing-dma-in-kmdf-drivers"></a>在 KMDF 驱动程序中测试 DMA


\[仅适用于 KMDF\]

以下工具可帮助调试支持 DMA 的基于框架的驱动程序：

-   [驱动程序验证程序](../devtest/driver-verifier.md) 包括检测各种 DMA 操作的不当使用的特定验证测试。 有关特定于 DMA 的验证的详细信息，请参阅 [Dma 验证](../devtest/dma-verification.md)。

-   [**！ Dma**](../debugger/-dma.md)内核调试器扩展显示有关 [驱动程序验证程序](../devtest/driver-verifier.md)正在验证的 dma 子系统和 dma 设备驱动程序的信息。

-   [内核模式驱动程序框架扩展](../debugger/kernel-mode-driver-framework-extensions--wdfkd-dll-.md)包含以下特定于 DMA 的命令：

    <a href="" id="-wdfcommonbuffer"></a>[**!wdfcommonbuffer**](../debugger/-wdfkd-wdfcommonbuffer.md)  
    转储有关给定公用缓冲区对象的信息。

    <a href="" id="-wdfdmaenabler"></a>[**!wdfdmaenabler**](../debugger/-wdfkd-wdfdmaenabler.md)  
    转储有关特定 DMA 启用程序对象及其事务和常见缓冲区对象的信息。

    <a href="" id="-wdfdmaenablers"></a>[**!wdfdmaenablers**](../debugger/-wdfkd-wdfdmaenablers.md)  
    列出所有 DMA 启用码及其事务和公用缓冲区对象。

    <a href="" id="-wdfdmatransaction"></a>[**!wdfdmatransaction**](../debugger/-wdfkd-wdfdmatransaction.md)  
    转储有关给定事务对象的信息。

 

