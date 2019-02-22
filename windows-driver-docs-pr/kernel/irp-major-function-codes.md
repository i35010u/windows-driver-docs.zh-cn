---
title: IRP 主要函数代码
description: IRP 主要函数代码
ms.date: 08/12/2017
ms.assetid: 11c5b1a9-74c0-47fb-8cce-a008ece9efae
ms.localizationpriority: medium
ms.openlocfilehash: c42a08cb8dab6ce5102d0a0e485a0a991936ea62
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546228"
---
# <a name="irp-major-function-codes"></a>IRP 主要函数代码





每个特定于驱动程序的 I/O 堆栈位置 (**IO\_堆栈\_位置**的主要函数代码，则它必须支持。

特定操作驱动程序将为给定**IRP\_MJ\_* XXX*** 代码依赖在某种程度上基础设备，尤其是对于[ **IRP\_MJ\_设备\_控制**](irp-mj-device-control.md)并[ **IRP\_MJ\_内部\_设备\_控件**](irp-mj-internal-device-control.md)请求。 例如，发送到键盘驱动程序的请求是一定某种程度上不同于发送到磁盘驱动程序。 但是，I/O 管理器定义的参数和 I/O 堆栈位置内容为每个系统定义主要函数代码。

每个更高级别的驱动程序必须设置 I/O 堆栈中适当的位置 Irp 的下一步低级驱动程序并调用[ **IoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff548336)，使用每个输入 IRP 或驱动程序创建 IRP (如果更高级别的驱动程序存储指针输入 IRP）。 因此，每个中间驱动程序必须提供基础的设备驱动程序处理每个主要的函数代码的调度例程。 否则为新的中间驱动程序将"中断链"每当应用程序或仍更高级别的驱动程序将尝试发送到基础设备驱动程序的 I/O 请求。

文件系统驱动程序还处理所需的系统定义子集**IRP\_MJ\_* XXX*** 函数代码，某些与从属**IRP\_MN\_* XXX*** 函数代码。

驱动程序处理 Irp 设置完成部分或全部以下主要函数代码：

[**IRP\_MJ\_CLEANUP**](irp-mj-cleanup.md)

[**IRP\_MJ\_CLOSE**](irp-mj-close.md)

[**IRP\_MJ\_CREATE**](irp-mj-create.md)

[**IRP\_MJ\_DEVICE\_CONTROL**](irp-mj-device-control.md)

[**IRP\_MJ\_文件\_系统\_控件**](irp-mj-file-system-control.md)

[**IRP\_MJ\_刷新\_缓冲区**](irp-mj-flush-buffers.md)

[**IRP\_MJ\_INTERNAL\_DEVICE\_CONTROL**](irp-mj-internal-device-control.md)

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)

[**IRP\_MJ\_POWER**](irp-mj-power.md)

[**IRP\_MJ\_查询\_信息**](irp-mj-query-information.md)

[**IRP\_MJ\_READ**](irp-mj-read.md)

[**IRP\_MJ\_SET\_INFORMATION**](irp-mj-set-information.md)

[**IRP\_MJ\_SHUTDOWN**](irp-mj-shutdown.md)

[**IRP\_MJ\_SYSTEM\_CONTROL**](irp-mj-system-control.md)

[**IRP\_MJ\_WRITE**](irp-mj-write.md)

在本部分中所述的输入和输出参数是在 IRP 的特定于函数的参数。

有关 Irp 的详细信息，请参阅[处理 Irp](https://msdn.microsoft.com/library/windows/hardware/ff546847)。

 

 




