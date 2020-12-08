---
title: 在框架外部处理 WDM IRP
description: 在框架外部处理 WDM IRP
keywords:
- WDM Irp WDK KMDF
- WDM Irp WDK KMDF，框架外
- Irp WDK KMDF
- KMDF-框架外的 Irp WDK
- I/o 请求数据包 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2666a24b15f10df243e2c319aafd8515e9240c25
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814729"
---
# <a name="handling-wdm-irps-outside-of-the-framework"></a>在框架外部处理 WDM IRP


\[仅适用于 KMDF\]

当 i/o 管理器将 i/o 请求数据包 (IRP) 到基于框架的驱动程序时，框架会截获 IRP，然后执行下列操作之一：

-   处理 IRP。 例如，框架处理包含 [**irp \_ mj \_ PNP**](../kernel/irp-mj-pnp.md) 和 [**irp \_ mj \_ POWER**](../kernel/irp-mj-power.md) 重大 i/o 函数代码的 irp。 处理这些 Irp 时，框架可能会通过调用驱动程序的事件回调函数与驱动程序通信。

-   为 IRP 创建框架请求对象，并将请求对象传递给驱动程序的一个 i/o 队列，以便驱动程序可以接收该对象（通常在请求处理程序中），并对其进行处理。 框架以这种方式处理读取、写入和设备 i/o 控制请求。

-   如果你的驱动程序是筛选器驱动程序，则将 IRP 传递到下一个较低的驱动程序 (如果你的驱动程序是筛选器驱动程序) ，或如果你的驱动程序不是筛选器) 驱动程序，则以状态 "无效设备请求 (" 的状态值完成 IRP， \_ \_ \_ 因为 IRP 包含框架不支持的 i/o 函数代码。

有时，驱动程序必须处理框架不支持的 i/o 函数代码。

通常，驱动程序可能需要在框架处理 IRP 之前对其进行预处理，或者驱动程序在框架和低级驱动程序完成处理后可能需要 postprocess IRP。

在预处理过程中，驱动程序可能需要将 IRP 转发到特定的 i/o 队列。

以下主题介绍了这些情况：

-   [处理框架不支持的 IRP](handling-an-irp-that-the-framework-does-not-support.md)
-   [对 IRP 进行预处理和后处理](preprocessing-and-postprocessing-irps.md)
-   [将 IRP 调度到 I/O 队列](dispatching-irps-to-i-o-queues.md)

 

