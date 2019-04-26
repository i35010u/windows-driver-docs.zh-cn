---
title: I/O 控制代码的缓冲区说明
description: I/O 控制代码的缓冲区说明
ms.assetid: a458f3fb-a6c7-42ae-870e-1617a96b496f
keywords:
- I/O 控制代码 WDK 内核，缓冲区说明
- 控制代码 WDK Ioctl，缓冲区说明
- Ioctl WDK 内核，缓冲区说明
- 缓冲说明 WDK Ioctl
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d8af2d869f1f3760affb5afcc083e30cf48549d5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63326045"
---
# <a name="buffer-descriptions-for-io-control-codes"></a>I/O 控制代码的缓冲区说明





I/O 控制代码包含在[ **IRP\_MJ\_设备\_控制**](https://msdn.microsoft.com/library/windows/hardware/ff550744)并[ **IRP\_MJ\_内部\_设备\_控件**](https://msdn.microsoft.com/library/windows/hardware/ff550766)请求。 I/O 管理器创建这些请求作为对的调用结果[ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216) （Microsoft Windows SDK 文档中所述） 和[ **IoBuildDeviceIoControlRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548318)。

因为[ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216)并**IoBuildDeviceIoControlRequest**接受输入的缓冲区和输出缓冲区作为参数，所有**IRP\_MJ\_设备\_控制**并**IRP\_MJ\_内部\_设备\_控制**请求提供这两个输入缓冲区和输出缓冲区。 系统描述这些缓冲区的方法是依赖于数据传输类型。 通过指定的传输类型*留空，则*中的值[ **CTL\_代码**](defining-i-o-control-codes.md)宏创建 IOCTL 代码值。

系统描述为每个缓冲区*留空，则*值，如下所示：

<a href="" id="method-buffered"></a>方法\_缓冲  
对于此传输类型，Irp 提供指向在缓冲区的指针**Irp-&gt;AssociatedIrp.SystemBuffer**。 此缓冲区表示输入的缓冲区和对的调用中指定的输出缓冲区[ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216)并**IoBuildDeviceIoControlRequest**。 该驱动程序传输数据，然后到此缓冲区。

对于输入数据，指定缓冲区大小**Parameters.DeviceIoControl.InputBufferLength**中的驱动程序[ **IO\_堆栈\_位置**](https://msdn.microsoft.com/library/windows/hardware/ff550659)结构。 用于输出数据缓冲区大小由指定**Parameters.DeviceIoControl.OutputBufferLength**中的驱动程序**IO\_堆栈\_位置**结构。

系统将为单个输入/输出缓冲区分配的空间大小为较大的两个长度值。

<a href="" id="method-in-direct-or-method-out-direct"></a>方法\_IN\_直接访问或通过方法\_出\_直接  
对于这些传输类型，Irp 提供指向在缓冲区的指针**Irp-&gt;AssociatedIrp.SystemBuffer**。 这表示对的调用中指定的输入的缓冲区**DeviceIoControl**并**IoBuildDeviceIoControlRequest**。 通过指定的缓冲区大小**Parameters.DeviceIoControl.InputBufferLength**中的驱动程序**IO\_堆栈\_位置**结构。

对于这些传输类型，Irp 还提供指向在 MDL **Irp-&gt;MdlAddress**。 这表示对的调用中指定的输出缓冲区[ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216)并**IoBuildDeviceIoControlRequest**。 但是，此缓冲区可以实际用作输入的缓冲区或输出缓冲区，按如下所示：

-   方法\_IN\_直接指定处理 IRP 的驱动程序是否被调用时在缓冲区中接收了数据。 输入的缓冲区，并指定方法，介绍了 MDL\_IN\_直接可确保正在执行的线程具有读取访问的缓冲区。

-   方法\_出\_直接指定是否处理 IRP 的驱动程序会将数据写到缓冲区之前完成 IRP。 输出缓冲区，并指定方法，介绍了 MDL\_出\_直接可确保正在执行的线程具有写访问的缓冲区。

有关这两种传输类型， **Parameters.DeviceIoControl.OutputBufferLength**指定描述 MDL 缓冲区的大小。

<a href="" id="method-neither"></a>方法\_NEITHER  
I/O 管理器不提供任何系统缓冲区或 MDLs。 IRP 提供到指定的输入和输出缓冲区的用户模式虚拟地址**DeviceIoControl**或**IoBuildDeviceIoControlRequest**，而不验证或将其映射。

输入的缓冲区的地址提供的**Parameters.DeviceIoControl.Type3InputBuffer**中的驱动程序**IO\_堆栈\_位置**结构和输出缓冲区通过指定地址**Irp-&gt;UserBuffer**。

由提供的缓冲区大小**Parameters.DeviceIoControl.InputBufferLength**并**Parameters.DeviceIoControl.OutputBufferLength**中的驱动程序**IO\_堆栈\_位置**结构。

有关详细信息**CTL\_代码**宏和传输类型上方列出，请参阅[定义的 I/O 控制代码](defining-i-o-control-codes.md)。

 

 




