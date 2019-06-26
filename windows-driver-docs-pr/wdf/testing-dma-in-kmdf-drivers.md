---
title: 在 KMDF 驱动程序中测试 DMA
description: 在 KMDF 驱动程序中测试 DMA
ms.assetid: 1D37F8B3-EAFC-4BB0-988D-64ADF30DBC40
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b65bcead90da7d014fab74eae5b6b66b3046f79
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372318"
---
# <a name="testing-dma-in-kmdf-drivers"></a>在 KMDF 驱动程序中测试 DMA


\[仅适用于 KMDF\]

以下工具可帮助调试基于框架的驱动程序支持 DMA 的：

-   [驱动程序验证程序](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)包括检测错误地使用各种 DMA 操作的特定验证测试。 有关特定于 DMA 的验证的详细信息，请参阅[DMA 验证](https://docs.microsoft.com/windows-hardware/drivers/devtest/dma-verification)。

-   [ **！ Dma** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-dma)内核调试器扩展显示 DMA 子系统和 DMA 的设备驱动程序验证的信息[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)。

-   [内核模式驱动程序框架扩展](https://docs.microsoft.com/windows-hardware/drivers/debugger/kernel-mode-driver-framework-extensions--wdfkd-dll-)包括以下特定于 DMA 的命令：

    <a href="" id="-wdfcommonbuffer"></a>[ **!wdfcommonbuffer**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfcommonbuffer)  
    转储有关给定的常见缓冲区对象的信息。

    <a href="" id="-wdfdmaenabler"></a>[ **!wdfdmaenabler**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdmaenabler)  
    转储有关特定 DMA 启用程序对象和其事务和公共缓冲区对象的信息。

    <a href="" id="-wdfdmaenablers"></a>[ **!wdfdmaenablers**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdmaenablers)  
    列出所有的 DMA 实现方法及其事务和公共缓冲区对象。

    <a href="" id="-wdfdmatransaction"></a>[ **!wdfdmatransaction**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdmatransaction)  
    转储有关给定的事务对象的信息。

 

 





