---
title: 基于 SerCx2 的串行控制器驱动程序的功能
description: 基于 SerCx2 的串行控制器驱动程序是一种 KMDF 驱动程序，它使用 KMDF 中的方法和回调执行一般的驱动程序操作，并与 SerCx2 通信以执行特定于串行控制器驱动程序的操作。
ms.date: 05/13/2019
ms.localizationpriority: medium
ms.openlocfilehash: e96f42862d5eb7a5b9f6dc8c17a47e771f3e09fa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805035"
---
# <a name="features-of-sercx2-based-serial-controller-drivers"></a>基于 SerCx2 的串行控制器驱动程序的功能

SerCx2 是对 Kernel-Mode Driver Framework (KMDF) 的扩展，它具有支持串行控制器驱动程序的特殊功能。 有关 KMDF 的详细信息，请参阅 [使用 WDF 开发驱动程序](../wdf/using-the-framework-to-develop-a-driver.md) SerCx2 的串行控制器驱动程序是一个 KMDF 驱动程序，该驱动程序使用 KMDF 中的方法和回调执行一般的驱动程序操作，并与 SerCx2 通信以执行特定于串行控制器驱动程序的操作。

通常，串行控制器在硬件级别兼容，16550通用异步接收器/发送器 (UART) 设备。 自个人计算初期以来使用了 UARTs 来控制台式计算机的情况下的串行端口。 最近，串行控制器包含在芯片 (SoC) 集成线路上的系统中，以提供与其他集成线路的低 pin 计数通信。 在基于 SoC 的硬件平台中，客户端发送 i/o 请求的 "串行端口" 只是 SoC 芯片上的一组串行接口 pin。 有关详细信息，请参阅 [串行控制器驱动程序概述](serial-drivers-overview.md)。

Microsoft 可能会为具有相似硬件功能的串行控制器系列提供串行控制器驱动程序。 或者，具有特殊功能的串行控制器的硬件供应商可能会提供自定义串行控制器驱动程序来支持这些功能。

串行控制器驱动程序通过设备驱动程序接口与 SerCx2 通信， (DDI) 。 SerCx2 DDI 分为两部分：

- 由 SerCx2 实现并由串行控制器驱动程序调用的一组驱动程序支持方法。
- 由串行控制器驱动程序实现并由 SerCx2 调用的一组事件回调函数。

有关 SerCx2 DDI 中方法和回调的详细说明，请参阅 [sercx 标头](/windows-hardware/drivers/ddi/sercx/) 主题中的版本 2 Serial Framework Extension (SerCx2) 参考。

尽管硬件供应商可以选择编写独立的串行控制器驱动程序，但执行此操作需要很大的努力。 相比之下，开发使用 SerCx2 的串行控制器驱动程序更容易，并且通常会导致驱动程序更小且更可靠。

SerCx2 代表控制器驱动程序管理以下任务：

- 读取和写入操作
- 串行 i/o 超时检测
- 硬件事件
- 如果支持系统 DMA 事务，系统 DMA 会传输 () 
- 与低功耗设备状态之间的转换
- 取消 i/o 请求 (在自定义 i/o 事务期间除外) 

若要管理读写操作，SerCx2 会将客户端中的 [**irp \_ mj \_ read**](/previous-versions/ff546883(v=vs.85)) 和 [**IRP \_ mj \_ 写入**](/previous-versions/ff546904(v=vs.85)) 请求转换为相对简单的 i/o 事务，以便串行控制器驱动程序进行处理。 有关详细信息，请参阅 [SerCx2 I/o 事务所](sercx2-i-o-transactions.md)。

SerCx2 作为名为 Sercx2.sys 的组件包含在 Windows 中。 串行控制器驱动程序静态链接到 SerCx2 库，Sercxstubs (版本 2.0) ，在运行时，将与 Sercx2.sys 通信。 SerCx2 DDI 是在 2.0 \\ Sercx 头文件中定义的。 Windows 8.1 的 Windows 驱动程序工具包中提供了 Sercxstubs 和 Sercx。
