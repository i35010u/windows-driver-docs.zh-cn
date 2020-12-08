---
title: IRP 主要函数代码
description: IRP 主要函数代码
ms.date: 03/09/2020
ms.localizationpriority: medium
ms.openlocfilehash: 4dadced74c85d25d62e96eebb0e9e22c7765b190
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801697"
---
# <a name="irp-major-function-codes"></a>IRP 主要函数代码


每个 [**IRP**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp) ([**IO_STACK_LOCATION**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)) 的每个特定于驱动程序的 i/o 堆栈位置都包含一个 (IRP_MJ_XXX) 的主要函数代码，该代码告诉驱动程序它或基础设备驱动程序应执行哪些操作来满足 i/o 请求。 每个内核模式驱动程序必须为它必须支持的主要功能代码提供调度例程。

驱动程序针对给定 **IRP \_ mj \_ <em>XXX</em>** 代码执行的特定操作依赖于基础设备，尤其是对于 [**IRP \_ mj \_ 设备 \_ 控制**](irp-mj-device-control.md)和 [**irp \_ mj \_ 内部 \_ 设备 \_ 控制**](irp-mj-internal-device-control.md)请求。 例如，发送到键盘驱动程序的请求一定与发送到磁盘驱动程序的请求有些不同。 但是，i/o 管理器为每个系统定义的主要函数代码定义参数和 i/o 堆栈位置内容。

每个更高级别的驱动程序都必须在 Irp 中为下一级驱动程序设置相应的 i/o 堆栈位置，并使用每个输入 IRP 来调用 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)，或者使用驱动程序创建的 irp (如果较高级别的驱动程序保留到输入 IRP) 上。 因此，每个中间驱动程序必须为基础设备驱动程序处理的每个主要函数代码提供一个调度例程。 否则，每当应用程序或更高级别的驱动程序尝试将 i/o 请求发送到基础设备驱动程序时，新的中间驱动程序就会 "中断链"。

文件系统驱动程序还处理系统定义的 **irp \_ MJ \_ <em>xxx</em>** 函数代码的必需子集，其中一些部分具有从属 **irp \_ MN \_ <em>xxx</em>** 函数代码。

驱动程序通过下列部分或全部主要功能代码来处理 Irp 集：

[**IRP \_ MJ \_ 清除**](irp-mj-cleanup.md)

[**IRP \_ MJ \_ 关闭**](irp-mj-close.md)

[**IRP \_ MJ \_ 创建**](irp-mj-create.md)

[**IRP \_ MJ \_ 设备 \_ 控制**](irp-mj-device-control.md)

[**IRP \_ MJ \_ 文件 \_ 系统 \_ 控制**](irp-mj-file-system-control.md)

[**IRP \_ MJ \_ 刷新 \_ 缓冲区**](irp-mj-flush-buffers.md)

[**IRP \_ MJ \_ 内部 \_ 设备 \_ 控制**](irp-mj-internal-device-control.md)

[**IRP \_ MJ \_ PNP**](irp-mj-pnp.md)

[**IRP \_ MJ \_ POWER**](irp-mj-power.md)

[**IRP \_ MJ \_ 查询 \_ 信息**](irp-mj-query-information.md)

[**IRP \_ MJ \_ 读取**](irp-mj-read.md)

[**IRP \_ MJ \_ 设置 \_ 信息**](irp-mj-set-information.md)

[**IRP \_ MJ \_ 关闭**](irp-mj-shutdown.md)

[**IRP \_ MJ \_ 系统 \_ 控件**](irp-mj-system-control.md)

[**IRP \_ MJ \_ 写入**](irp-mj-write.md)

本节中所述的输入和输出参数是 IRP 中特定于函数的参数。

有关 Irp 的详细信息，请参阅 [处理 irp](./handling-irps.md)。

 

