---
title: I/O 堆栈位置
description: I/O 堆栈位置
ms.assetid: 62c8ee00-c7cb-4aa1-90ab-b8bedbd818ee
keywords:
- Irp WDK 内核，I/O 堆栈位置
- I/O 堆栈位置 WDK 内核
- 堆栈位置 WDK 内核
- 分层驱动程序 I/O 堆栈位置 WDK 内核
- Irp WDK 内核内容
- IO_STACK_LOCATION 结构
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ae09b1cddf0813a586a499b5f2c360011eeffc27
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545492"
---
# <a name="io-stack-locations"></a>I/O 堆栈位置





I/O 管理器提供的分层驱动程序链中每个驱动程序 I/O 堆栈位置设置了每个 IRP。 每个 I/O 堆栈位置组成[ **IO\_堆栈\_位置**](https://msdn.microsoft.com/library/windows/hardware/ff550659)结构。

I/O 管理器创建的每个 IRP 的 I/O 堆栈位置的数组与数组元素对应的分层驱动程序链中每个驱动程序。 每个驱动程序拥有的堆栈位置中的数据包和调用之一[ **IoGetCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff549174)以获取有关 I/O 操作的特定于驱动程序的信息。

此类链中的每个驱动程序负责调用[ **IoGetNextIrpStackLocation**](https://msdn.microsoft.com/library/windows/hardware/ff549266)，然后设置下一步低驱动程序的 I/O 堆栈位置。 此外可以使用任何更高级别的驱动程序的 I/O 堆栈位置来存储有关操作的上下文，以便在驱动程序[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例程可以执行其清理操作。

[分层驱动程序中处理 Irp](example-i-o-request---the-details.md#ddk-example-i-o-request---the-details-kg)图在原始 IRP 中显示两个 I/O 堆栈位置，因为它显示了两个驱动程序、 文件系统驱动程序和大容量存储设备驱动程序。 在驱动程序分配 Irp[分层驱动程序中处理 Irp](example-i-o-request---the-details.md#ddk-example-i-o-request---the-details-kg)图没有所需的堆栈位置 FSD 创建它们。 将 Irp 为较低级别的驱动程序分配任何更高级别的驱动程序还可以确定多少个 I/O 堆栈位置应具有新 Irp，根据**StackSize**下一步低驱动程序的设备对象的值。

下图显示了更详细地的 IRP 的内容。

![说明在 irp i/o 堆栈位置的内容的关系图](images/2irpios.png)

如图所示，IRP 中每个特定于驱动程序的 I/O 堆栈位置包含以下常规信息：

- 主要函数代码 (**IRP\_MJ\_* XXX * * *)，该驱动程序的基本操作，该值指示应执行

- 有关处理 FSDs、 更高级别的 SCSI 驱动程序和所有即插即用驱动程序的一些主要函数代码，次要函数代码 (**IRP\_MN\_* XXX * * *)，指示的基本操作的子情况驱动程序应执行

- 一组特定于操作的参数，例如长度和启动的驱动程序在其中或从中将数据传输的缓冲区的位置

- 指向表示请求的操作的目标 （物理、 逻辑，或虚拟） 设备的驱动程序创建的设备对象的指针

- 指向表示打开的文件、 设备、 目录或卷的文件对象的指针

  文件系统驱动程序通过其在 Irp 的 I/O 堆栈位置访问的文件对象。 其他驱动程序通常忽略的文件对象。

组的特定驱动程序处理的 IRP 主要和次要函数代码可以是特定于设备类型。 但是，最低级别的驱动程序和中间驱动程序 （包括即插即用的函数和筛选器驱动程序） 通常处理的基本请求以下组：

-   [**IRP\_MJ\_创建**](https://msdn.microsoft.com/library/windows/hardware/ff550729) — 打开，指示它已存在且可用的 I/O 操作的目标设备对象

-   [**IRP\_MJ\_读取**](https://msdn.microsoft.com/library/windows/hardware/ff550794) — 从设备传输数据

-   [**IRP\_MJ\_编写**](https://msdn.microsoft.com/library/windows/hardware/ff550819) — 将数据传输到设备

-   [**IRP\_MJ\_设备\_控件**](https://msdn.microsoft.com/library/windows/hardware/ff550744) — 设置 （或重置） 设备，根据系统定义的特定于设备的类型的 I/O 控制代码 (IOCTL)

-   [**IRP\_MJ\_关闭**](https://msdn.microsoft.com/library/windows/hardware/ff550720) — 关闭目标设备对象

-   [**IRP\_MJ\_PNP**](https://msdn.microsoft.com/library/windows/hardware/ff550772) — 插对设备执行操作。 **IRP\_MJ\_PNP**通过 I/O 管理器的即插即用管理器发送请求。

-   [**IRP\_MJ\_电源**](https://msdn.microsoft.com/library/windows/hardware/ff550784) — 执行电源操作在设备上的。 **IRP\_MJ\_POWER**电源管理器通过 I/O 管理器发送请求。

有关驱动程序所需处理主要 IRP 函数代码的详细信息，请参阅[IRP 主要函数代码](https://msdn.microsoft.com/library/windows/hardware/ff550710)。

一般情况下，I/O 管理器将发送 Irp 到大容量存储设备驱动程序的至少两个 I/O 堆栈位置与因为文件系统上层的其他大容量存储设备的驱动程序。 I/O 管理器将 Irp 发送与任何具有它的上面没有其他驱动程序的驱动程序的堆栈位置。

但是，I/O 管理器为在系统中将新的驱动程序添加到现有的驱动程序的任何链提供支持。 例如，中间*镜像驱动程序*备份指定的磁盘分区上的数据可能要插入的驱动程序，如文件系统驱动程序和中所示的最低级别驱动程序对之间[中处理 Irp分层驱动程序](example-i-o-request---the-details.md#ddk-example-i-o-request---the-details-kg)图。 当此新的驱动程序将自身附加到设备堆栈时，I/O 管理器来调整 I/O 堆栈中的位置发送到文件系统、 镜像和最低级别的驱动程序的所有 Irp 数。 每个 IRP 的中的文件系统[分层驱动程序中处理 Irp](example-i-o-request---the-details.md#ddk-example-i-o-request---the-details-kg)图分配也会包含此类的新镜像驱动程序的另一个 I/O 堆栈位置。

请注意，此支持将新的驱动程序添加到现有链意味着到 Irp 中的 I/O 堆栈位置的任何特定驱动程序的访问权限的某些限制：

- 分层驱动程序的链中的更高级别的驱动程序可以安全地仅访问其自己和任何 IRP 中的下一步低级驱动程序的 I/O 堆栈位置。 此类驱动程序必须设置 Irp 中的下一步低级驱动程序的 I/O 堆栈位置。 但是，在设计此类的更高级别的驱动程序时，无法预测新的驱动程序时 （或是否） 将添加到您的驱动程序正下方的现有链。

  因此，应假定任何后来添加驱动程序将处理相同的 IRP 主要函数代码 (**IRP\_MJ\_* XXX * * *) 移位后的下一步低级驱动程序一样。

- 分层驱动程序的链中的最低级别驱动程序可以安全地访问仅其自己 I/O 堆栈的位置中任何 IRP。 在设计时这样的驱动程序，您不能预测新的驱动程序时 （或是否） 将添加到现有的链上面您的设备驱动程序。

  在设计时的最低级别驱动程序，假定该驱动程序可以继续处理 Irp 使用传递在其自己 I/O 堆栈位置中，任何给定 IRP 的原始源的信息，但其上方的分层许多驱动程序。

 

 




