---
title: SerCx2 体系结构概述
description: SerCx2 一起使用的串行控制器驱动程序，以允许外围设备的驱动程序和串行连接的外围设备之间进行通信。
ms.assetid: BA5D8966-ACC5-44ED-8CB8-61D1BCF39522
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b568e09c87923ac88c4b80725d66fa8748e60b81
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548130"
---
# <a name="sercx2-architectural-overview"></a>SerCx2 体系结构概述


SerCx2 一起使用的串行控制器驱动程序，以允许外围设备的驱动程序和串行连接的外围设备之间进行通信。 通常情况下，串行控制器已集成到芯片 (SoC) 芯片上的系统与外部 SoC 芯片但焊接到相同的印刷电路板的外围设备提供低 pin 计数通信。

下图显示了串行连接的外围设备和设备的驱动程序之间的通信路径。 此外围设备的驱动程序在内核模式或用户模式下运行，并将 I/O 请求发送到外围设备连接到串行端口。

![块 sercx2 和关联的组件示意图](images/sercx2modules.png)

SerCx2 和串行控制器驱动程序同时在内核模式下运行并通过 SerCx2 设备驱动程序接口 (DDI) 相互通信。 串行控制器驱动程序将调用由 SerCx2 实现的驱动程序支持方法。 SerCx2 调用事件回叫函数，实现串行控制器驱动程序。

通常，串行控制器的硬件寄存器是内存映射。 串行控制器驱动程序直接访问这些寄存器可配置的串行端口，并将数据传入和传出连接到串行端口的外围设备。 对于较长的数据传输，SerCx2 通常使用 DMA 传输 （不在上图中所示）。

外围设备驱动程序需要打开外围设备的逻辑连接信息将封装在一种特殊类型的硬件资源，通过调用*连接 ID*。 有关详细信息，请参阅[按顺序连接到外围设备的连接 Id](connection-ids-for-serially-connected-peripheral-devices.md)。

通常情况下，驱动程序 I/O 请求将直接发送到串行控制器。 当在用户模式应用程序需要进行通信按顺序连接的外围设备，与外围设备行为的驱动程序作为应用程序和设备之间的中介。 如果应用程序需要将数据传入或从外围设备，应用程序发送执行写入操作 ([**IRP\_MJ\_编写**](https://msdn.microsoft.com/library/windows/hardware/ff546904)) 请求或读取 ([ **IRP\_MJ\_读取**](https://msdn.microsoft.com/library/windows/hardware/ff546883)) 到外围设备驱动程序，并通过将相应的写入或读取的请求发送到串行控制器外围设备驱动程序响应请求。 此外，外围设备驱动程序可以发送设备 I/O 控制请求 (Ioctl) 可配置的串行端口。 Ioctl SerCx2 支持的列表，请参阅[串行 I/O 请求接口](serial-i-o-request-interface.md)。

将 I/O 请求发送到串行控制器的外围设备驱动程序是使用任一一个内核模式驱动程序[内核模式驱动程序框架](https://msdn.microsoft.com/library/windows/hardware/ff544296)(KMDF)，或使用的用户模式驱动程序[用户模式驱动程序框架](https://msdn.microsoft.com/library/windows/hardware/ff560442) (UMDF)。 SerCx2 管理发送到串行控制器的外围设备驱动程序的 I/O 请求的队列。

读取或写入请求的响应，SerCx2 启动串行控制器和在请求中的数据缓冲区之间移动数据的一个或多个 I/O 事务。 每个 I/O 事务使用通过编程方式设置 I/O (PIO) 或 DMA 串行控制器和在请求中的数据缓冲区之间传输数据。 I/O 事务串行控制器驱动程序支持的类型取决于串行控制器的硬件功能。 有关详细信息，请参阅[SerCx2 I/O 事务的概述](overview-of-sercx2-i-o-transactions.md)。

 

 




