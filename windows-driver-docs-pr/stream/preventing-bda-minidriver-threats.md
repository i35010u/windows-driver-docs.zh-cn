---
title: 阻止 BDA 微型驱动程序威胁
description: 阻止 BDA 微型驱动程序威胁
keywords:
- 广播驱动程序体系结构 WDK AVStream，安全性
- BDA WDK AVStream，安全性
- 安全 WDK BDA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e418be47612486694180897ec96491cb5c9f4c93
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790149"
---
# <a name="preventing-bda-minidriver-threats"></a>阻止 BDA 微型驱动程序威胁





可以通过以下方式阻止可能 [引入到 BDA 微型驱动程序](introducing-threats-to-a-bda-minidriver.md) 中的威胁：

<a href="" id="threats-in-the-signal-transport-stream"></a>信号传输流中的威胁  
BDA 微型驱动程序不应解释信号负载的内容，因为此类内容可能是破坏性的。 BDA 微型驱动程序只应组合负载缓冲区，并将其传递到下一个筛选器。

 

如果 BDA 微型驱动程序解释有效负载，则在分析有效负载中的此类内容时，应仔细验证其内容。

<a href="" id="threats-from-special-purpose-ioctls"></a>来自特殊目的 IOCTLs 的威胁  
BDA 微型驱动程序不应将接口公开给允许这些应用程序直接控制总线、内存或任何其他硬件的应用程序。 因此，应从 BDA 微型驱动程序中删除所有专用 IOCTLs 的处理。 例如，IOCTLs 包括供应商创建的调试 IOCTLs。 为了处理此类 IOCTLs，BDA 微型驱动程序将实现 [**IRP \_ MJ \_ 设备 \_ 控制**](../kernel/irp-mj-device-control.md) 调度例程。

<a href="" id="threats-from-direct-wdm-dispatch-routines"></a>直接 WDM 调度例程的威胁  
BDA 微型驱动程序不应提供绕过内核流式处理 (KS) 类模型的 WDM 调度例程。 BDA 微型驱动程序应使用 KS 驱动程序的 AVStream 模块来提供 [调度](creating-dispatch-tables.md) 和 [自动化](defining-automation-tables.md) 例程，因为它还提供安全检查。 为了提供直接 WDM 调度例程，BDA 微型驱动程序将实现任何 [IRP 主要功能代码](../kernel/irp-major-function-codes.md)。

 

