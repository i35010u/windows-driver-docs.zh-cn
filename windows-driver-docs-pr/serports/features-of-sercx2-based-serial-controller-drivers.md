---
title: 基于 SerCx2 的串行控制器驱动程序的功能
description: SerCx2 基于串行控制器驱动程序是 KMDF 驱动程序的使用方法和回调中的 KMDF 执行通用驱动程序操作，并与 SerCx2 来执行特定于串行控制器驱动程序的操作的通信。
ms.assetid: 4A9B80F1-4DE1-4D35-ADDF-90058A4F8388
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b03ddf08716a55b06f4b2edb30505db950da1c0f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562452"
---
# <a name="features-of-sercx2-based-serial-controller-drivers"></a>基于 SerCx2 的串行控制器驱动程序的功能


SerCx2 是扩展[内核模式驱动程序框架](https://msdn.microsoft.com/library/windows/hardware/ff544296)(KMDF) 具有特殊功能，可支持串行控制器驱动程序。 SerCx2 基于串行控制器驱动程序是 KMDF 驱动程序的使用方法和回调中的 KMDF 执行通用驱动程序操作，并与 SerCx2 来执行特定于串行控制器驱动程序的操作的通信。

通常情况下，串行控制器是兼容的硬件级别与 16550 通用异步接收器/转换器 (UART) 设备。 UARTs 之后控制为个人计算技术的早期阶段的串行端口位于台式 Pc 的情况下使用。 最近，串行控制器提供低 pin 计数通信与其他集成电路芯片 (SoC) 集成线路上包含在系统中。 在 SoC 基于硬件的平台，客户端将 I/O 请求发送到的"串行端口"是只需一 SoC 芯片上的串行接口 pin。 有关详细信息，请参阅[串行控制器驱动程序概述](serial-drivers-overview.md)。

Microsoft 可能会提供一系列有类似的硬件功能的串行控制器的串行控制器驱动程序。 或者，具有特殊功能的串行控制器的硬件供应商可能提供自定义串行控制器驱动程序以支持这些功能。

通过设备驱动程序接口 (DDI) 与 SerCx2 通信，串行控制器驱动程序。 SerCx2 DDI 由两部分组成：

-   驱动程序支持方法实现的 SerCx2 和串行控制器驱动程序调用的一组。
-   事件回叫函数，由串行控制器驱动程序实现并由 SerCx2 调用一组。

有关方法和 SerCx2 DDI 中的回调的详细说明，请参阅[版本 2 串行框架扩展 (SerCx2) 引用](https://msdn.microsoft.com/library/windows/hardware/dn265349)。

尽管硬件供应商具有编写独立串行控制器驱动程序的选项，但需要大量精力来执行此操作。 比较而言，开发使用 SerCx2 串行控制器驱动程序更容易和通常会导致要小得多且更可靠的驱动程序。

SerCx2 管理代表控制器驱动程序的以下任务：

-   读取和写入操作
-   串行 I/O 超时检测
-   硬件事件
-   系统 DMA 传输 （如果支持系统 DMA 事务）
-   低功耗设备状态转换
-   取消 I/O 请求 （I/O 的自定义事务期间除外）

若要管理读取和写入操作，SerCx2 转换[ **IRP\_MJ\_读取**](https://msdn.microsoft.com/library/windows/hardware/ff546883)并[ **IRP\_MJ\_编写** ](https://msdn.microsoft.com/library/windows/hardware/ff546904)串行控制器驱动程序来处理来自为相对简单的 I/O 事务的客户端请求。 有关详细信息，请参阅[SerCx2 I/O 事务](sercx2-i-o-transactions.md)。

SerCx2 作为名为 Sercx2.sys 组件包含在 Windows 中。 串行控制器驱动程序以静态方式链接到 SerCx2 库，Sercxstubs.lib （2.0 版），并且，在运行时，与其通信 Sercx2.sys。 在 2.0 版中定义 SerCx2 DDI\\Sercx.h 标头文件。 Windows 驱动程序工具包的 Windows 8.1 中提供了 Sercxstubs.lib 和 Sercx.h。

 

 




