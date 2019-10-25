---
title: 基于 SerCx2 的串行控制器驱动程序的功能
description: 基于 SerCx2 的串行控制器驱动程序是一种 KMDF 驱动程序，它使用 KMDF 中的方法和回调执行一般的驱动程序操作，并与 SerCx2 通信以执行特定于串行控制器驱动程序的操作。
ms.assetid: 4A9B80F1-4DE1-4D35-ADDF-90058A4F8388
ms.date: 05/13/2019
ms.localizationpriority: medium
ms.openlocfilehash: 3246ff757f949cdc0c24a349414dbe21cd09eaf0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842445"
---
# <a name="features-of-sercx2-based-serial-controller-drivers"></a>基于 SerCx2 的串行控制器驱动程序的功能

SerCx2 是内核模式驱动程序框架（KMDF）的扩展，它具有支持串行控制器驱动程序的特殊功能。 有关 KMDF 的详细信息，请参阅[使用 WDF 开发驱动程序](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-the-framework-to-develop-a-driver)SerCx2 的串行控制器驱动程序是一个 KMDF 驱动程序，该驱动程序使用 KMDF 中的方法和回调执行一般的驱动程序操作，并与 SerCx2 通信以执行特定于串行控制器驱动程序的操作。

通常，串行控制器在硬件级别与16550通用异步接收器/发送器（UART）设备兼容。 自个人计算初期以来使用了 UARTs 来控制台式计算机的情况下的串行端口。 最近，串行控制器包含在芯片（SoC）集成线路上的系统中，以提供与其他集成线路的低 pin 计数通信。 在基于 SoC 的硬件平台中，客户端发送 i/o 请求的 "串行端口" 只是 SoC 芯片上的一组串行接口 pin。 有关详细信息，请参阅[串行控制器驱动程序概述](serial-drivers-overview.md)。

Microsoft 可能会为具有相似硬件功能的串行控制器系列提供串行控制器驱动程序。 或者，具有特殊功能的串行控制器的硬件供应商可能会提供自定义串行控制器驱动程序来支持这些功能。

串行控制器驱动程序通过设备驱动程序接口（DDI）与 SerCx2 通信。 SerCx2 DDI 分为两部分：

- 由 SerCx2 实现并由串行控制器驱动程序调用的一组驱动程序支持方法。
- 由串行控制器驱动程序实现并由 SerCx2 调用的一组事件回调函数。

有关 SerCx2 DDI 中方法和回调的详细说明，请参阅[sercx 标头](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/)主题中的版本2串行框架扩展（SerCx2）参考。

尽管硬件供应商可以选择编写独立的串行控制器驱动程序，但执行此操作需要很大的努力。 相比之下，开发使用 SerCx2 的串行控制器驱动程序更容易，并且通常会导致驱动程序更小且更可靠。

SerCx2 代表控制器驱动程序管理以下任务：

- 读取和写入操作
- 串行 i/o 超时检测
- 硬件事件
- 系统 DMA 传输（如果支持系统 DMA 事务）
- 与低功耗设备状态之间的转换
- 取消 i/o 请求（自定义 i/o 事务期间除外）

若要管理读写操作，SerCx2 将[**IRP\_\_mj**](https://docs.microsoft.com/previous-versions/ff546883(v=vs.85))转换为 "读取" 和 " [**IRP"\_mj\_** ](https://docs.microsoft.com/previous-versions/ff546904(v=vs.85))将客户端中的请求写入相对简单的 i/o 事务，以便串行控制器驱动程序进行处理。 有关详细信息，请参阅[SerCx2 I/o 事务所](sercx2-i-o-transactions.md)。

SerCx2 作为名为 Sercx2 的组件包含在 Windows 中。 串行控制器驱动程序静态链接到 SerCx2 库 Sercxstubs （版本2.0），并在运行时与 Sercx2 通信。 SerCx2 DDI 在 2.0\\Sercx 标头文件中定义。 Windows 8.1 的 Windows 驱动程序工具包中提供了 Sercxstubs 和 Sercx。
