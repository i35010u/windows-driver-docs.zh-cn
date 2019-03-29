---
title: 在 KMDF 驱动程序中测试 DMA
description: 在 KMDF 驱动程序中测试 DMA
ms.assetid: 1D37F8B3-EAFC-4BB0-988D-64ADF30DBC40
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c1f02897021ee80b3c3bea917968efda609303e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563108"
---
# <a name="testing-dma-in-kmdf-drivers"></a>在 KMDF 驱动程序中测试 DMA


\[仅适用于 KMDF\]

以下工具可帮助调试基于框架的驱动程序支持 DMA 的：

-   [驱动程序验证程序](https://msdn.microsoft.com/library/windows/hardware/ff545448)包括检测错误地使用各种 DMA 操作的特定验证测试。 有关特定于 DMA 的验证的详细信息，请参阅[DMA 验证](https://msdn.microsoft.com/library/windows/hardware/ff544915)。

-   [ **！ Dma** ](https://msdn.microsoft.com/library/windows/hardware/ff562369)内核调试器扩展显示 DMA 子系统和 DMA 的设备驱动程序验证的信息[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)。

-   [内核模式驱动程序框架扩展](https://msdn.microsoft.com/library/windows/hardware/ff551876)包括以下特定于 DMA 的命令：

    <a href="" id="-wdfcommonbuffer"></a>[**!wdfcommonbuffer**](https://msdn.microsoft.com/library/windows/hardware/ff565679)  
    转储有关给定的常见缓冲区对象的信息。

    <a href="" id="-wdfdmaenabler"></a>[**!wdfdmaenabler**](https://msdn.microsoft.com/library/windows/hardware/ff565717)  
    转储有关特定 DMA 启用程序对象和其事务和公共缓冲区对象的信息。

    <a href="" id="-wdfdmaenablers"></a>[**!wdfdmaenablers**](https://msdn.microsoft.com/library/windows/hardware/ff565719)  
    列出所有的 DMA 实现方法及其事务和公共缓冲区对象。

    <a href="" id="-wdfdmatransaction"></a>[**!wdfdmatransaction**](https://msdn.microsoft.com/library/windows/hardware/ff565721)  
    转储有关给定的事务对象的信息。

 

 





