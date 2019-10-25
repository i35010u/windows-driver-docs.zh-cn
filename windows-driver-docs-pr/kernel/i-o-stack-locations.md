---
title: I/O 堆栈位置
description: I/O 堆栈位置
ms.assetid: 62c8ee00-c7cb-4aa1-90ab-b8bedbd818ee
keywords:
- Irp WDK 内核，i/o 堆栈位置
- I/o 堆栈位置 WDK 内核
- 堆栈位置 WDK 内核
- 分层驱动程序 i/o 堆栈位置 WDK 内核
- Irp WDK 内核，内容
- IO_STACK_LOCATION 结构
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 35a645f822d9259f425ebce38b4bf4486cbf93c1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838650"
---
# <a name="io-stack-locations"></a>I/O 堆栈位置





I/o 管理器为分层驱动程序链中的每个驱动程序提供它所设置的每个 IRP 的 i/o 堆栈位置。 每个 i/o 堆栈位置都包含[**IO\_堆栈\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)结构。

I/o 管理器将为每个 IRP 创建一个 i/o 堆栈位置数组，其中的数组元素对应于一系列分层驱动程序中的每个驱动程序。 每个驱动程序都拥有数据包中的一个堆栈位置，并调用[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)来获取有关 i/o 操作的特定于驱动程序的信息。

此类链中的每个驱动程序都负责调用[**IoGetNextIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetnextirpstacklocation)，并设置下一个较低的驱动程序的 i/o 堆栈位置。 任何更高级别的驱动程序的 i/o 堆栈位置也可用于存储有关操作的上下文，以便驱动程序的[*IoCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程可以执行其清理操作。

[分层驱动程序中的处理 irp](example-i-o-request---the-details.md#ddk-example-i-o-request---the-details-kg)显示了原始 IRP 中的两个 i/o 堆栈位置，因为它显示了两个驱动程序：文件系统驱动程序和大容量存储设备驱动程序。 [分层驱动程序的处理 irp](example-i-o-request---the-details.md#ddk-example-i-o-request---the-details-kg)中的驱动程序分配的 irp 没有创建它们的 FSD 的堆栈位置。 为较低级别的驱动程序分配 Irp 的任何更高级别的驱动程序也根据下一个较低驱动程序的设备对象的**StackSize**值确定新的 irp 应具有的 i/o 堆栈位置数量。

下图更详细地显示了 IRP 的内容。

![说明 irp 中 i/o 堆栈位置内容的关系图](images/2irpios.png)

如图所示，IRP 中每个特定于驱动程序的 i/o 堆栈位置都包含以下常规信息：

- 主要函数代码（**IRP\_MJ\_* XXX * * *），指示驱动程序应执行的基本操作

- 对于由 FSDs、较高级别的 SCSI 驱动程序和所有 PnP 驱动程序处理的主要函数代码，一种次要函数代码（**IRP\_MN\_* XXX * * *），指示驱动程序应执行的基本操作的 subcase

- 一组特定于操作的参数，如缓冲区的长度和起始位置，驱动程序从该缓冲区传输数据

- 指向驱动程序创建的设备对象的指针，该对象表示请求的操作的目标（物理、逻辑或虚拟）设备

- 指向文件对象的指针，该对象表示打开的文件、设备、目录或卷

  文件系统驱动程序通过 Irp 中的 i/o 堆栈位置访问 file 对象。 其他驱动程序通常会忽略文件对象。

特定驱动程序处理的 IRP 主要和次要函数代码集可以是特定于设备类型的。 但是，最低级别驱动程序和中间驱动程序（包括 PnP 函数和筛选器驱动程序）通常处理以下基本请求集：

-   [**IRP\_MJ\_创建**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create) -打开目标设备对象，指示该对象存在并且可用于 i/o 操作

-   [**IRP\_MJ\_读取**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read) -从设备传输数据

-   [**IRP\_MJ\_写入**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write) -将数据传输到设备

-   [**IRP\_MJ\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control) -根据系统定义的设备类型特定 i/o 控制代码（IOCTL）设置（或重置）设备

-   [**IRP\_MJ\_关闭**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-close) -关闭目标设备对象

-   [**IRP\_MJ\_PNP**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp) —在设备上执行即插即用操作。 **IRP\_MJ\_pnp**请求由 pnp 管理器通过 i/o 管理器发送。

-   [**IRP\_MJ\_电源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power) -在设备上执行电源操作。 由电源管理器通过 i/o 管理器发送**IRP\_MJ\_power** request。

有关需要驱动程序处理的主要 IRP 函数代码的详细信息，请参阅[IRP 主要功能代码](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-major-function-codes)。

通常，i/o 管理器将至少有两个 i/o 堆栈位置的 Irp 发送到大容量存储设备驱动程序，因为文件系统与大容量存储设备的其他驱动程序分层。 I/o 管理器将具有单个堆栈位置的 Irp 发送到任何没有层次之上的其他驱动程序的驱动程序。

但是，i/o 管理器支持将新驱动程序添加到系统中现有驱动程序的任何链。 例如，可能会在一对驱动程序（如文件系统驱动程序和[分层驱动程序的处理 irp 中](example-i-o-request---the-details.md#ddk-example-i-o-request---the-details-kg)所示的最低级别驱动程序）之间插入一个可在给定磁盘分区上备份数据的中间*镜像驱动程序*。 当此新驱动程序将自身附加到设备堆栈时，i/o 管理器会在它发送到文件系统、镜像和最低级别驱动程序的所有 Irp 中调整 i/o 堆栈位置的数目。 每个 IRP，分配的[分层驱动程序中处理 irp](example-i-o-request---the-details.md#ddk-example-i-o-request---the-details-kg)的文件系统也将包含此类新镜像驱动程序的另一个 i/o 堆栈位置。

请注意，此支持将新驱动程序添加到现有的链中，这会对任何特定驱动程序对 Irp 中 i/o 堆栈位置的访问有一定的限制：

- 分层驱动程序链中的较高级别的驱动程序只能安全访问其自己的和下一个较低级别的驱动程序在任何 IRP 中的 i/o 堆栈位置。 此类驱动程序必须为 Irp 中的下一级驱动程序设置 i/o 堆栈位置。 但是，在设计此类较高级别的驱动程序时，不能预测将新的驱动程序添加到驱动程序正下方的现有链的时间。

  因此，您应假设任何后续添加的驱动程序都将处理相同的 IRP 主要功能代码（**irp\_MJ\_* XXX * * *），因为下一级驱动程序已被替换。

- 分层驱动程序链中的最低级别驱动程序只能安全访问任何 IRP 中自己的 i/o 堆栈位置。 设计此类驱动程序时，不能预测是否会将新驱动程序添加到设备驱动程序上的现有链中。

  在设计最低级别的驱动程序时，假定驱动程序可以使用在其自己的 i/o 堆栈位置传入的信息继续处理 Irp，无论给定 IRP 的源源和多个驱动程序在其之上分层。

 

 




