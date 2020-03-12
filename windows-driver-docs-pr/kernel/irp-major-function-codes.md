---
title: IRP 主要函数代码
description: IRP 主要函数代码
ms.date: 03/09/2020
ms.assetid: 11c5b1a9-74c0-47fb-8cce-a008ece9efae
ms.localizationpriority: medium
ms.openlocfilehash: 17cb9101cc034c0f1cd58b7142c4c70750284793
ms.sourcegitcommit: 8c898615009705db7633649a51bef27a25d72b26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2020
ms.locfileid: "78935392"
---
# <a name="irp-major-function-codes"></a>IRP 主要函数代码


每个[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)的每个特定于驱动程序的 i/o 堆栈位置（[**IO_STACK_LOCATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)）都包含一个主要函数代码（IRP_MJ_XXX），该代码告诉驱动程序它或基础设备驱动程序应执行哪些操作来满足 i/o 请求。 每个内核模式驱动程序必须为它必须支持的主要功能代码提供调度例程。

驱动程序为给定的**IRP\_MJ\_<em>XXX</em>** 代码执行的特定操作在某种程度上依赖于基础设备，尤其是对于[**IRP\_MJ\_设备\_控件**](irp-mj-device-control.md)和[**irp\_** ](irp-mj-internal-device-control.md)\_\_\_ 例如，发送到键盘驱动程序的请求一定与发送到磁盘驱动程序的请求有些不同。 但是，i/o 管理器为每个系统定义的主要函数代码定义参数和 i/o 堆栈位置内容。

每个更高级别的驱动程序都必须在 Irp 中为下一级驱动程序设置相应的 i/o 堆栈位置，并使用每个输入 IRP 或使用驱动程序创建的 IRP （如果较高级别的驱动程序保存到输入 IRP）调用[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)。 因此，每个中间驱动程序必须为基础设备驱动程序处理的每个主要函数代码提供一个调度例程。 否则，每当应用程序或更高级别的驱动程序尝试将 i/o 请求发送到基础设备驱动程序时，新的中间驱动程序就会 "中断链"。

文件系统驱动程序还处理系统定义的**IRP\_MJ\_<em>XXX</em>** 函数代码的必需子集，某些部分使用从属**IRP\_MN\_<em>XXX</em>** 函数代码。

驱动程序通过下列部分或全部主要功能代码来处理 Irp 集：

[**IRP\_MJ\_清除**](irp-mj-cleanup.md)

[**IRP\_MJ\_关闭**](irp-mj-close.md)

[**IRP\_MJ\_创建**](irp-mj-create.md)

[**IRP\_MJ\_设备\_控件**](irp-mj-device-control.md)

[**IRP\_MJ\_文件\_系统\_控件**](irp-mj-file-system-control.md)

[**IRP\_MJ\_刷新\_缓冲区**](irp-mj-flush-buffers.md)

[**IRP\_MJ\_内部\_设备\_控制**](irp-mj-internal-device-control.md)

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)

[**IRP\_MJ\_POWER**](irp-mj-power.md)

[**IRP\_MJ\_查询\_信息**](irp-mj-query-information.md)

[**IRP\_MJ\_读取**](irp-mj-read.md)

[**IRP\_MJ\_集\_信息**](irp-mj-set-information.md)

[**IRP\_MJ\_关闭**](irp-mj-shutdown.md)

[**IRP\_MJ\_系统\_控件**](irp-mj-system-control.md)

[**IRP\_MJ\_写入**](irp-mj-write.md)

本节中所述的输入和输出参数是 IRP 中特定于函数的参数。

有关 Irp 的详细信息，请参阅[处理 irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-irps)。

 

 




