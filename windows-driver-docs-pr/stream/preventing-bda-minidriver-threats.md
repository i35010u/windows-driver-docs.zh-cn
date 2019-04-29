---
title: 阻止 BDA 微型驱动程序威胁
description: 阻止 BDA 微型驱动程序威胁
ms.assetid: 090cd2fb-d35b-4c42-a90d-a0d567d4b93f
keywords:
- 广播驱动程序体系结构 WDK AVStream 安全性
- BDA WDK AVStream 安全性
- 安全 WDK BDA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ccf41dca6a72fb46dfafd2cc0b0144cdf4c87a1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362217"
---
# <a name="preventing-bda-minidriver-threats"></a>阻止 BDA 微型驱动程序威胁





可以是威胁[BDA 微型驱动程序中引入](introducing-threats-to-a-bda-minidriver.md)可以防止在以下方面：

<a href="" id="threats-in-the-signal-transport-stream"></a>信号传输流中的威胁  
BDA 微型驱动程序不应将信号有效负载的内容，因为此类内容可以是破坏性。 BDA 微型驱动程序应仅集合负载的缓冲区，并将它们传递到下一个筛选器。

 

如果 BDA 微型驱动程序解释有效负载，它们应仔细验证这些内容，分析此类内容从有效负载时。

<a href="" id="threats-from-special-purpose-ioctls"></a>特殊用途 Ioctl 的潜在威胁  
BDA 微型驱动程序不应公开的接口连接到允许的总线、 内存或任何其他硬件的直接控制这些应用程序的应用程序。 因此，应从 BDA 微型驱动程序中删除所有特殊用途 Ioctl 的处理。 例如，此类 Ioctl 包括供应商创建调试 Ioctl。 若要处理此类 Ioctl，BDA 微型驱动程序会实现[ **IRP\_MJ\_设备\_控制**](https://msdn.microsoft.com/library/windows/hardware/ff550744)调度例程。

<a href="" id="threats-from-direct-wdm-dispatch-routines"></a>从直接 WDM 威胁调度例程  
BDA 微型驱动程序不应提供 WDM 调度例程，跳过的内核流式处理 (KS) 类模型。 BDA 微型驱动程序应使用 KS 驱动程序的 AVStream 模块提供[调度](creating-dispatch-tables.md)并[自动化](defining-automation-tables.md)例程因为它还提供了安全检查。 若要提供直接 WDM 调度例程，BDA 微型驱动程序将实现的任何[IRP 主要函数代码](https://msdn.microsoft.com/library/windows/hardware/ff550710)。

 

 




