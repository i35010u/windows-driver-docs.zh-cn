---
title: SerCx2 体系结构概述
description: SerCx2 与串行控制器驱动程序一起工作，可在外围设备驱动程序与串行连接外围设备之间进行通信。
ms.assetid: BA5D8966-ACC5-44ED-8CB8-61D1BCF39522
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b08bc721b818853e9e32c8b58cf78df8096faae
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186943"
---
# <a name="sercx2-architectural-overview"></a>SerCx2 体系结构概述

SerCx2 与串行控制器驱动程序一起工作，可在外围设备驱动程序与串行连接外围设备之间进行通信。 通常情况下，串行控制器集成到芯片 (SoC) 芯片上的系统中，以提供与 SoC 芯片外部设备不同但焊接到相同印刷电路板的外部设备的低 pin 计数通信。

下图显示了串行连接外围设备与此设备的驱动程序之间的通信路径。 此外设驱动程序在内核模式或用户模式下运行，并将 i/o 请求发送到外围设备连接到的串行端口。

![sercx2 和关联组件的块示意图](images/sercx2modules.png)

SerCx2 和串行控制器驱动程序都在内核模式下运行，并通过 SerCx2 设备驱动程序接口 (DDI) 彼此进行通信。 串行控制器驱动程序调用由 SerCx2 实现的驱动程序支持方法。 SerCx2 调用由串行控制器驱动程序实现的事件回调函数。

通常，串行控制器的硬件寄存器是内存映射的。 串行控制器驱动程序直接访问这些寄存器，以配置串行端口，并将数据传入和传出连接到串行端口的外围设备。 对于较长的数据传输，SerCx2 通常使用 DMA 传输 (前面的关系图中未显示) 。

外围设备驱动程序需要打开到外围设备的逻辑连接的信息封装在一种特殊类型的硬件资源中，称为 *连接 ID*。 有关详细信息，请参阅 [连接 id 以进行串行连接的外围设备](connection-ids-for-serially-connected-peripheral-devices.md)。

通常，只有驱动程序会直接将 i/o 请求发送到串行控制器。 用户模式应用程序需要与串行连接的外围设备通信时，该设备的外围设备驱动程序将充当应用程序和设备之间的中介。 如果应用程序需要将数据传入或传出外围设备，应用程序将发送写入 ([**IRP \_ mj \_ 写入**](/previous-versions/ff546904(v=vs.85))) 请求，或读取 ([**irp \_ mj \_ 读取**](/previous-versions/ff546883(v=vs.85))) 请求，并将相应的写入或读取请求发送到串行控制器。 此外，外围设备驱动程序可以 (IOCTLs) 发送设备 i/o 控制请求来配置串行端口。 有关 SerCx2 支持的 IOCTLs 列表，请参阅 [串行 I/o 请求接口](serial-i-o-request-interface.md)。

将 i/o 请求发送到串行控制器的外围设备驱动程序可以是使用 [内核模式驱动程序框架](../wdf/using-the-framework-to-develop-a-driver.md) (KMDF) 的内核模式驱动程序，也可以是使用 [用户模式驱动程序框架](../wdf/overview-of-the-umdf.md) (UMDF) 的用户模式驱动程序。 SerCx2 管理外设驱动程序发送到串行控制器的 i/o 请求队列。

为了响应读取或写入请求，SerCx2 启动了一个或多个 i/o 事务，以便在串行控制器与请求中的数据缓冲区之间移动数据。 每个 i/o 事务均使用程控 i/o (PIO) 或 DMA 在串行控制器和请求中的数据缓冲区之间传输数据。 串行控制器驱动程序支持的 i/o 事务类型取决于串行控制器的硬件功能。 有关详细信息，请参阅 [SerCx2 I/o 事务概述](overview-of-sercx2-i-o-transactions.md)。